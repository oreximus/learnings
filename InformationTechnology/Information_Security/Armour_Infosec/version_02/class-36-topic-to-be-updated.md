# Notes

## Topic: ACLs in Linux

- ACLs allow the admin to define (or extend) the access (permissions) to the particular files or directory
  between distinct users.

- `Standard Permissions`: permission bits per users/groups (users, group and others).
- `Extended Permissions`: Allows specifying permissions for multiple users and groups.
- `Supported filesystem`: Filesystem like, ext3, ext4 and XFS. They all supports ACL, if
  `ACL` option is enabled.

### Enabling ACLs

- in the `/etc/fstab` file:
  - select the filesystem, and the put `acl` beside `defaults` option separated by comma.

- Installing ACL

- In `RHEL` distros:

```
yum install acl
```

- Reboot your system, to load the changed settings in `/etc/fstab`.

### Applying ACLs

- to display the ACLs:

```
getfacl dir-name
```

### Additional

- alternative tool: `chacl`

### Next Topics:

- `su` and `sg`

# Class 02

## Topic: Hosting

### Shared Hosting

- Where resources are shared between different clients, and this is
  managed by the Hosting Provider.

### Self Hosting

- Provie the complete resource access to the clients.
- Good for managing large number of customers.

### Dedicated Hosting

- Provide the complete server resources access from the admin level to
  the client.

### VPS (Virtual Private Server):

- Dividing the single server into multiple virtual servers and then
  allocate them to the clients (with complete access).

### Shared Hosting

- Dividing complete server into various parts and then distribute
  it the client.

- Good for less number of visitors.

### Cloud Hosting

-

#### Additional

- `To Study`: IIS
