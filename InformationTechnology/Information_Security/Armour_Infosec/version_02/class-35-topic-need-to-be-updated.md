# Class 01

## Topic: Set Group ID

**Main usage**:

- **On directories**:

```
chmor g+s data
```

- sample scenario:
  - creating some users: (around 3 users)
  - making them the members of EMP group:

  ```
  gpasswd -A user1 EMP
  ```

- changing the group access of the directory:

```
chgrp EMP dir-name
```

```
chmod 775 dir-name
```

- to be able get access to the files and directory created by any users
  who belongs to the group

```
chmod g+s dir-name
```

- for removing access:

```
chmod g-s dir-name
```

- from the octal mode:

```
chmod 2775 dir-name
```

### Sticky Bit

- applying stick bit:

```
chmod o+t dir-name
```

- applying from the octal way:

```
chmod 1777 dir-name
```

## To Study:

- ACLs (access control list)
