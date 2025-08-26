# Class 34

## Topic: Disk-Quota-Management in Linux

- for installing quota:
  - debian based distros:

  ```
  apt install quota
  ```

  - RHEL based distros:

  ```
  dnf install quota
  ```

### Implementing the quota in /etc/fstab

-

- command to mount the disk:

```
mount -a
```

- command to check the quota:

```
quotacheck -cum /d1
```

```
quotacheck -
```

- enabling quota:

```
xfs
```

- quota editing commands:

```
edquota -
```
