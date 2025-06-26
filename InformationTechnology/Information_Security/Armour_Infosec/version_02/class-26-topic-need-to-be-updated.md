# Class 01

## Topic: awk command:

- awk structure:

```
awk 'BEGIN { ... }
           { ... }
     END   { ... }
'
```

- data between the single quotes will always be the main section.

- printing fields:

- printing first field separated by space:

```
awk '{print $1}' /etc/passwd
```

- printing first field separated by colon:

```
awk -F: '{print $1}' /etc/passwd
```

- printing 1st and 7th column of `passwd`:

```
awk -F: '{print $1,$7}' /etc/passwd
```

- filtering particular pattern via awk:

- complete line printing from the passwd file matching with root pattern:

```
awk -F: '/root/{print $0}' /etc/passwd
```

- only printing the 7th column of the root matching pattern in passwd:

```
awk -F: '/root/{print $7}' /etc/passwd
```

**ifconfig example**:

- printing the inet details:

```
ifconfig | awk '/inet/{print}'
```

- printing the second field matching, containing IP usually:

```
ifconfig | awk '/inet /{print $2}'
```

- printing the IP output with BEGIN and END section:

```
ifconfig | awk 'BEGIN {print "----------IFCONFIG--------"}/inet /{print $2} END {print "----------END--------"}'
```

# Class 02

## Topic: NTFS Permissions:

- 

## Drive Permissions:

- for opening the system drive, on the run dialog:

```
%systemdrive%
```

**Default Permissions**:

- users Permission Table:
    - `SYSTEM`: Full Control
    - `Administrators`: Full Control
    - `Users`: Read & Execute List Folder Contents, Read
    - `Authenticated Users`: Modify, Read and Execute
    - `Users`: Read and Execute Only (No modification power)
