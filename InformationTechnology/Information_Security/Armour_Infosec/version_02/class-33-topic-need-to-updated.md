# Class 01

## Topic: Important Users files in Linux

### `/etc/passwd` file:

- `first field (username)`: login name (username)
- `second field (x)`: indicate the actual password is stored in `/etc/shadow`.
- `third field (UID)`: User Id: `0` is root, `1000+` are normal usersA.
- `fourth field (GID)`: Same as UID
- `fifth field (comment)`: user's real name or info.
- `sixth field (home directory)`: Default login directory.
- `seventh field (shell)`: Default shell (e.g.`/bin/bash, /sbin/nologin`)


### `/etc/shadow` file:

- mainly stores our passwords, our security settings.

- fields:
    - 1. username
    - 2. encrypted password
    - 3. last_changed
    - 4. min
    - 5. max 
    - 6. warn
    - 7. inactive
    - 8. expire
    - 9. unused

### `/etc/group` file:

- field:
    1. group_name
    2. x: placeholder of the encrypted password (rarely used)
    3. GID
    4. user_list (number of members)

- getting group information:

```
getent group <group-name>
```

**output**(i.e. getting group details for `sudo`)
![class33img01](assets/images/class33img01.png)


### `/etc/gshadow` file:

- to view the content of the file:

```
sudo cat /etc/gshadow
```

- In the field 2 (encrypted password):
    - `!` and `!!` means the password is not configured.
    - `*` disabled can't use this


