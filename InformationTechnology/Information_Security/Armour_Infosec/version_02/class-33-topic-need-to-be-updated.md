# Class 01

## Topic: Disk Management: Swap Extending

- "Swap extend", refers to the process of increasing or extending the size of the swap space on
  a computer.

- common commands: `swapon`, `swapoff`

### swap size:

- System with 2GB Ram,
- System with 2 or 4GB RAM, equivalent swap space.
- System with more than 8GB or more RAM, at least 4GB of swap

### Command to check space in linux:

- provide the information in human readable form (better option).

```
free -h
```

- provide the information with size in megabytes.

```
free -m
```

- provide the information with size in kilobytes.

```
free -k
```

- provide the information with size in gigabytes.

```
free -g
```

-

### View active swap devices

- lists active swap partitions :

```
swapon
```

- summary of swap spaces:

```
swapon -s
```

### Common commands:

- use `lsblk` to list created partitions.

- creating swap from the swap formatted partition:

```
mkswap /dev/your-partition
```

- to enable the swap in linux:

```
swapon
```

- Make swap persistent:

```
vim /etc/fstab

UUID=66c1b829-862b-405f-9815-66836d15ee8d defaults 0 0
UUID=66c1b829-899b-405f-9815-66836d15ee8d defaults 0 0
UUID=66c1b829-889b-763f-9815-66836d15ee8d defaults 0 0
```

> After performing persistent extending swap, remember to reboot.
