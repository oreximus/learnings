# Class 01:

## Topic: LVM (Logical Volume Management)

- Make your disk dynamic,

### Understanding the LVM:

- if you have a single disk,

- doing RAID 0 by combining all of the disks together, and make single performance disk.
  But if single volume fails the entire data or disk may get corrupted.

### Key Components:

1. Physical Volume (PVs)
2. Volume Groups (VGs)
3. Logical Volumes (LVs)

### Essential Features:

- `Dynamic Resizing`

### Commands for LVM:

- installing lvm:

```
# for debian based distro
sudo apt install lvm2
```

```
# for RHEL based distros
sudo yum install lvm2
```

- for checking physical volume:

```
pvs
```

```
pvdisplay
```

- creating pysical volumes:

```
pvcreate <your-disk-name>
```

### Commands to checkout:

- `vgs`
- `lvcreate` or lvm related all commands

#### Extra Instructions:

- create logical volumes and then format them with `mkfs`
- you can format the disk in the filesystem (i.e. xfs,ext4)
- then you can mount the created disk.
- for mounting disk permanently, you need to the permanent entries in the `/etc/fstab`.

#### Practical Instructions:

- creating LVMs
- extending and shrinking LVMs.
- extending volumes via normal LVM extending will not be formatted,
  for that you need to use `resize2fs`
- for shrinking volumes you need to `unmount` the volumes first.
- first manually resize the data volume, to avoid data loss on using `lvresize`.
- removing lvm via `lvremove` and to remove volume group `vgremove` and for physical volume `pvremove`, you can check
  them via `lvs`, `vgs` and `pvs` respectively.

#### RAID Practical Instructions:

> mdadm: Multiple Disk and Device Administration

- using `mdadm` command for implementing RAID with it's levels in the disk.
- complete the process from Creating RAID, formatting them, and the configure them to start
  using it.
- after creating RAID, check the RAID status:

```
mdadm --detail /dev/md0
```

- for stopping RAID, `unmount` your first and the stop them via:

```
mdadm --stop /dev/your-raid-partition
```
