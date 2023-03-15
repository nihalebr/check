---
layout: ../../layouts/BlogPost.astro
title: Logical Volume Manager (LVM) 💽
description: LVM is a logical volume manager for the Linux kernel that allows
  you to manage disk storage. It is a device mapper target that provides logical
  volume management for the Linux kernel.
publishDate: 2023-03-16T00:00:56.801Z
heroImage: /assets/placeholder-hero.jpg
---



## About LVM
LVM combines multiple physical disk drives into a single “virtual” drive (Volume group). This virtual drive can then be divided into one or more logical volumes. Each logical volume can be formatted with a filesystem and mounted as a separate drive.

## Advantages of LVM

* LVM allows you to easily add or remove storage space to a system without having to reconfigure the filesystem.

* Keeping the filesystem separate from the physical storage allows you to easily move the filesystem to a different physical storage device.

* LVM allows you to easily resize the filesystem without having to reconfigure the filesystem.

## Disadvantages of LVM

* LVM is not a filesystem. It is a logical volume manager. It does not provide any filesystem features.

* LVM does not provide any data protection features. You need to use a filesystem that provides data protection features.




## Usage

Before creation of a Physical Volume, you need to create a partition on the disk. You can use fdisk or gdisk to create a partition.
(or you can use a whole disk as a Physical Volume).

### Create a Physical Volume
```bash
pvcreate /dev/sda2 /dev/sdb2
```
After creating a Physical Volume, you can create a Volume Group.

### Create a Volume Group
```bash
vgcreate vg0 /dev/sda2 /dev/sdb2
```

Finally, you can create a Logical Volume.To create a Logical Volume, you need to specify the size of the Logical Volume. You can specify the size in megabytes (MB), gigabytes (GB), or terabytes (TB). Also, you can specify the size as No. of Physical Extents (PEs).

### Create a Logical Volume using size in MB or GB
```bash
lvcreate -L 100GB -n lv0 vg0
```
### Create a Logical Volume using No. of Physical Extents (PEs)
```bash
lvcreate -l 100 -n lv0 vg0
```

After creating a Logical Volume, you can format it with a filesystem and mount it.
