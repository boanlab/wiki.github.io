---
title: Release apt-get Locks
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Configuration

```
sudo rm /var/lib/apt/lists/lock
sudo rm /var/cache/apt/archives/lock
sudo rm /var/lib/dpkg/lock
sudo rm /var/cache/debconf/config.dat
```

```
sudo dpkg --configure -a
```

```
sudo apt-get update
sudo apt-get upgrade
```

