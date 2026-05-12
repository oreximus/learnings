Here is a detailed **Technical Design Document (TDD)** derived from the requirements in your PowerPoint file. This document expands the slides into an actionable blueprint for development.

---

# Technical Design Document: Appointment Scheduling & Reminder System

## 1. Purpose & Scope

**Purpose**  
Build a production-ready, scalable healthcare appointment orchestration platform supporting patients, doctors, care managers, and admins. Phase-1 MVP focuses on core scheduling + reminders.

**Scope**

- Doctor discovery & availability management
- Real-time slot booking, reschedule, cancel
- Multi-channel reminders (Push, Email, SMS, WhatsApp)
- Audit logging & compliance (DPDP)
- Async, scalable notification delivery

---

## 2. System Architecture

### 2.1 High-Level Architecture Diagram (Text Representation)

```
[Patient App]      [Doctor App]      [Admin Dashboard]
       |                  |                   |
       └──────────────────┼───────────────────┘
                    API Gateway (Kong/Tyk)
                            |
            ┌───────────────┼───────────────┐
            |               |               |
    [Auth Service]   [Appointment Service]  [User Service]
            |               |               |
            └───────────────┼───────────────┘
                      Event Bus (RabbitMQ)
                            |
            ┌───────────────┼───────────────┐
            |               |               |
    [Reminder Engine]  [Notification Service]  [Audit Service]
            |               |
      [Redis]         [Firebase/Twilio]
```

### 2.2 Service Breakdown

| Service              | Responsibility                         | Tech                       |
| -------------------- | -------------------------------------- | -------------------------- |
| API Gateway          | Auth, rate limiting, routing           | Kong / Go‑Kit              |
| Auth Service         | JWT, RBAC                              | Go + JWT                   |
| User Service         | Patient/Doctor/Admin profiles          | Go, PostgreSQL             |
| Appointment Service  | Slot mgmt, booking, reschedule, cancel | Go, PostgreSQL, Redis lock |
| Reminder Engine      | Schedule & retry reminders             | Go, RabbitMQ, Redis        |
| Notification Service | Send via Firebase/Twilio               | Go + HTTP clients          |
| Audit Service        | Log all scheduling ops                 | Go + PostgreSQL / S3       |

### 2.3 Async Flows

- Appointment creation → event published → Reminder Engine schedules job.
- Notification failures → retry queue (exponential backoff).

---

## 3. Database Design

### 3.1 Entity Relationship Diagram (Core Tables)

```sql
-- Users (common profile)
CREATE TABLE users (
    id UUID PRIMARY KEY,
    name TEXT NOT NULL,
    role TEXT NOT NULL, -- patient, doctor, care_manager, admin
    phone TEXT,
    email TEXT UNIQUE,
    created_at TIMESTAMP
);

-- Doctors (role-specific)
CREATE TABLE doctors (
    id UUID PRIMARY KEY REFERENCES users(id),
    specialization TEXT,
    timezone TEXT NOT NULL
);

-- Availability (recurring or single slots)
CREATE TABLE availabilities (
    id UUID PRIMARY KEY,
    doctor_id UUID REFERENCES doctors(id),
    start_time TIMESTAMP NOT NULL,
    end_time TIMESTAMP NOT NULL,
    is_recurring BOOLEAN DEFAULT false,
    recurrence_rule TEXT -- RFC 5545 (optional)
);

-- Appointments
CREATE TABLE appointments (
    id UUID PRIMARY KEY,
    patient_id UUID REFERENCES users(id),
    doctor_id UUID REFERENCES doctors(id),
    slot_start TIMESTAMP NOT NULL,
    slot_end TIMESTAMP NOT NULL,
    status TEXT NOT NULL, -- scheduled, confirmed, cancelled, completed
    payment_status TEXT,
    created_at TIMESTAMP,
    updated_at TIMESTAMP,
    version INT DEFAULT 1 -- for optimistic locking
);

-- Reminders
CREATE TABLE reminders (
    id UUID PRIMARY KEY,
    appointment_id UUID REFERENCES appointments(id),
    channel TEXT NOT NULL, -- push, email, sms, whatsapp
    scheduled_time TIMESTAMP NOT NULL,
    sent_time TIMESTAMP,
    status TEXT DEFAULT 'pending', -- pending, sent, failed
    retry_count INT DEFAULT 0
);

-- Audit Logs
CREATE TABLE audit_logs (
    id UUID PRIMARY KEY,
    user_id UUID,
    action TEXT,
    entity_type TEXT, -- appointment, availability
    entity_id UUID,
    old_state JSONB,
    new_state JSONB,
    created_at TIMESTAMP
);
```

### 3.2 Indexing Strategy

- `appointments(doctor_id, slot_start)` for slot lookup
- `appointments(patient_id, status)` for patient history
- `reminders(scheduled_time, status)` for reminder dispatcher
- `availabilities(doctor_id, start_time)`

---

## 4. API Planning

### 4.1 Authentication

All APIs require `Authorization: Bearer <JWT>` with RBAC.

### 4.2 Appointment Service APIs

| Method | Endpoint                              | Description             | Roles                         |
| ------ | ------------------------------------- | ----------------------- | ----------------------------- |
| GET    | `/api/v1/doctors/:id/slots?date=...`  | Get available slots     | patient, doctor, care_manager |
| POST   | `/api/v1/appointments`                | Book appointment        | patient                       |
| GET    | `/api/v1/appointments/:id`            | Get appointment details | patient, doctor, admin        |
| PUT    | `/api/v1/appointments/:id/reschedule` | Reschedule              | patient, care_manager         |
| DELETE | `/api/v1/appointments/:id/cancel`     | Cancel                  | patient, doctor, admin        |
| GET    | `/api/v1/patients/:id/appointments`   | History                 | patient, care_manager         |

**Request/Response Example (Book Appointment)**

```json
POST /api/v1/appointments
{
  "doctor_id": "uuid",
  "slot_start": "2026-05-20T10:00:00Z",
  "slot_end": "2026-05-20T10:30:00Z",
  "payment_method": "insurance"
}

Response 201:
{
  "appointment_id": "uuid",
  "status": "scheduled",
  "confirmation_deadline": "2026-05-19T10:00:00Z"
}
```

### 4.3 Doctor Availability APIs

| Method | Endpoint                           | Description |
| ------ | ---------------------------------- | ----------- |
| POST   | `/api/v1/doctors/availability`     | Add slot    |
| GET    | `/api/v1/doctors/availability`     | List slots  |
| DELETE | `/api/v1/doctors/availability/:id` | Remove slot |

### 4.4 Notification API (Internal)

| Method | Endpoint                       | Description                               |
| ------ | ------------------------------ | ----------------------------------------- |
| POST   | `/internal/notifications/send` | Send reminder (called by Reminder Engine) |

---

## 5. Concurrency & Conflict Prevention

### Problem

Two patients booking same slot → double booking.

### Solution: Distributed Locking (Redis)

```pseudo
FUNCTION book_appointment(doctor_id, slot_start, patient_id):
    lock_key = "lock:slot:" + doctor_id + ":" + slot_start
    IF redis.setnx(lock_key, ttl=5s):
        try:
            IF slot NOT booked in DB:
                INSERT appointment
                COMMIT
                RETURN success
            ELSE:
                RETURN conflict
        finally:
            redis.del(lock_key)
    ELSE:
        RETRY with backoff
```

Also use **optimistic locking** with `version` column on `appointments` table as fallback.

---

## 6. Reminder Engine Design

### 6.1 Workflow

1. Appointment created → event published to `reminder.schedule` queue.
2. Reminder Engine consumes → calculates reminder times (e.g., 24h, 1h before).
3. Inserts rows into `reminders` table.
4. Scheduler cron (every minute) picks pending reminders where `scheduled_time <= NOW()`.
5. Sends to Notification Service via queue.
6. On failure → retry with backoff (max 3 attempts), then mark `failed`.

### 6.2 Retry Policy

- Retry delays: 1min, 5min, 30min
- Dead-letter queue after 3 failures → manual alert.

### 6.3 Channel Mapping

| Channel  | Provider         | Retry |
| -------- | ---------------- | ----- |
| Push     | Firebase FCM     | Yes   |
| Email    | SMTP / SendGrid  | Yes   |
| SMS      | Twilio           | Yes   |
| WhatsApp | Twilio / Gupshup | Yes   |

---

## 7. Security & Compliance (DPDP)

| Control           | Implementation                                           |
| ----------------- | -------------------------------------------------------- |
| Authentication    | JWT, short expiry, refresh token                         |
| RBAC              | User role in JWT; middleware checks per endpoint         |
| Data encryption   | TLS for transport; AES-256 for PII at rest               |
| Audit logging     | All scheduling actions logged (who, when, old/new state) |
| Session handling  | HTTP-only cookies or secure token storage                |
| Data minimization | Logs exclude patient medical data                        |

---

## 8. Scalability Approach

| Component       | Scaling method                                        |
| --------------- | ----------------------------------------------------- |
| Appointment API | Horizontal scaling (Kubernetes HPA)                   |
| PostgreSQL      | Read replicas + connection pooling (PgBouncer)        |
| Redis           | Cluster mode for distributed locks                    |
| RabbitMQ        | Multiple consumers per queue                          |
| Reminder Engine | Partition reminders by `scheduled_time` date sharding |

**Auto-scaling trigger:** CPU > 70% or queue length > 1000 messages.

---

## 9. Error Handling & Resilience

| Scenario             | Mitigation                                           |
| -------------------- | ---------------------------------------------------- |
| Slot conflict        | Return 409 Conflict + retry instruction              |
| Notification failure | Retry queue + alert on dead-letter                   |
| DB down              | Circuit breaker → fallback read replica              |
| High traffic         | Rate limiting (100 req/min per user)                 |
| Timezone mismatch    | Store all timestamps in UTC; convert per user in app |

---

## 10. Implementation Roadmap (MVP Focus)

| Phase                          | Milestones                                                                 | Duration |
| ------------------------------ | -------------------------------------------------------------------------- | -------- |
| **Phase 1** (Core scheduling)  | Availability API, Book/Reschedule/Cancel, PostgreSQL schema, Redis locking | 4 weeks  |
| **Phase 2** (Reminder engine)  | Reminder scheduler, RabbitMQ, Firebase + Twilio integration, retry logic   | 3 weeks  |
| **Phase 3** (Integrations)     | Audit logging, DPDP compliance, API Gateway                                | 2 weeks  |
| **Phase 4** (Testing & deploy) | Load testing, security review, staging → production                        | 2 weeks  |

---

## 11. Success Metrics (Observability)

| Metric                      | Target  | Instrumentation     |
| --------------------------- | ------- | ------------------- |
| Booking success rate        | >99.5%  | Prometheus counter  |
| Reminder delivery success   | >98%    | per-channel metrics |
| No-show reduction           | 30% ↓   | compare appt status |
| Avg booking completion time | <10 sec | latency histogram   |

**Dashboards:** Grafana + Loki logs + Tempo traces.

---

## 12. Risks & Mitigation (From Slides + Additions)

| Risk                  | Mitigation                                       |
| --------------------- | ------------------------------------------------ |
| Slot conflicts        | Redis distributed lock + optimistic locking      |
| Notification failures | Retry engine + dead-letter queue alert           |
| High traffic spike    | HPA + rate limiting + async queue                |
| Timezone mismatch     | UTC storage + user timezone preference           |
| DPDP violation        | Audit logs + encryption + access control reviews |

---

## 13. Conclusion

This design translates your PPT into a **developer-ready blueprint** with:

- Microservice boundaries
- Concrete database schema
- API contracts
- Concurrency handling
- Async reminder pipeline
- Security & compliance ready for Phase‑1 MVP

**Next Step:** Create repository per service, set up Kubernetes namespace, and implement `Appointment Service` as the first deliverable.
