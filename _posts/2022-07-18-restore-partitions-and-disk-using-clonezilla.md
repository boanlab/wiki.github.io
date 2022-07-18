---
title: Restore Partitions and Disks using Clonezilla
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Commands

- Download Clonezilla

```
https://clonezilla.org/downloads/download.php?branch=stable
http://ko.softoware.net/apps/get-clonezilla-livecd-for-linux.html
```

- Create a Clonezilla Live USB

```
UltraISO - http://www.ezbsystems.com/ultraiso/download.htm
- Connect a USB drive to your PC
- Run UltraISO
[File] - [Open] - Clonezilla ISO file
[Bootable] - [Write Disk Image...] - [Write]
```

- Save a partition or a disk

```
Boot with the created USB drive
...
1) choose [device-image]
2) choose [local-dev]
3) choose the backup partition (not the target image!!!)
...
4) choose [Beginner mode]
5) choose either [savedisk] or [saveparts]
...
Follow the instructions on the screen
```

- Restore a partition or a disk

```
Boot with the created USB drive
...
1) choose [device-image]
2) choose [local-dev]
3) choose the backup partition (not the target image!!!)
...
4) choose [Beginner mode]
5) choose either [restoredisk] or [restoreparts]
...
Follow the instructions on the screen
```

