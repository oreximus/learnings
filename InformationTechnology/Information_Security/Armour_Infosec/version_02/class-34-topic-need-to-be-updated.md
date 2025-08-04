# Class 01

## Topic: User Management in Linux

- `useradd` command:

- displaying the useful files outputs (when creating new user):

```

```

- `/etc/default/useradd`:

```
# contains pre-defined useradd config
# useradd default file
GROUP-100
```

- defining the Home Directory location manually:

```
useradd u7 -d /backup/u7
```

- creating Home Directory in the defined location:

```
useradd u8 -m -d /backup/u8
```

- for avoiding creating home directory:

```
useradd u9 --no-create-home
```

- providing commenting while creating a user:

```
userad --comment "Test Comment" u10
```

"

- changing shell for the user:

```
useradd -s /bin/sh username
```

- proving the UID manually:

```
useradd -g 1011 username
```

- generating password hashes with `mkpasswd`:

```
mkpasswd -m sha-512
```

**output**:

```
$6$hHTcPdRQ9Wnumajg$0IzZtBR4wHGI1WE/1WabRTZkvkRSs1R8bykmkWrGHGfE.Vq5qu34tZl7BzBMo9hNttktHsgrlIWr9ou82OHfw1
```

- setting expiry of the user:

```
useradd u5 -e 2025-12-11
```

> practice to create user, practing setting UID, GID

# Class 02

## Topic: Applying Group Policies through ADDS

- disabling the regedit access
- disabling the cmd access
- disabling the c drive access

> we can create a the synced environment for the logged-users
> so that they have only access to the data that's provided to them
> from the server.

> login with local user(admin): .\Administrator(user)
