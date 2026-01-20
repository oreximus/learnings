# Notes for PostgreSQL common solutions:

## Changing or Resetting the the PostgreSQL password in linux:

- in your linux, edit file: `/etc/postgresql/<version>/main/pg_hba.conf`

- change the values to something like this:

```
# IPv4 local connections:
host    all             all             127.0.0.1/32            trust
# IPv6 local connections:
host    all             all             ::1/128                 trust
```

- and restart the postgresql service.

- then in your psql cli:

```
sudo -u postgres psql
```

- for changing password interactively:

```
\password postgres
```

- SQL for the password change, and put the your password in the place of
  `your_new_password`:

```
ALTER USER postgres WITH PASSWORD 'your_new_password';
```

- exit the psql shell by `\q`

- revert the changes in the `/etc/postgresql/<version>/main/pg_hba.conf` file to:

```
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
```

- and restart the postgresql service again

## Connecting PostgreSQL in NestJS

- Installing these packages:

```
npm install --save @nestjs/typeorm typeorm pg
npm install --save-dev @types/pg
```

- <D-5><D-5><D-5><D-5eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJmZGYzMDkwZi1kMTFmLTRiNWMtOTdmMi0wNmZjYTcyNThjYjMiLCJlbWFpbCI6InZpa3JhbS5rdW1hckBleGFtcGxlLmNvbSIsImZpcnN0TmFtZSI6IlZpa3JhbSIsImxhc3ROYW1lIjoiS3VtYXIiLCJpc0FkbWluIjpmYWxzZSwiaWF0IjoxNzY4OTQ1NDcwLCJleHAiOjE3NjkwMzE4NzB9.85LY4mPiauySQSwkG7ErebSU4aAuAyshE1kBfsH1Cvs>
