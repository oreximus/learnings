# Notes for PostgreSQL common solutions:

## Changing or Resetting the the PostgreSQL password in linux:

- in your linux, edit file: /etc/postgresql/<version>/main/pg_hba.conf

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

- revert the changes in the /etc/postgresql/<version>/main/pg_hba.conf file to:

```
# IPv4 local connections:
host    all             all             127.0.0.1/32            scram-sha-256
# IPv6 local connections:
host    all             all             ::1/128                 scram-sha-256
```

- and restart the postgresql service again
