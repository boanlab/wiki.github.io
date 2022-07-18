---
title: Modify the Login Method of Ubuntu Cloud Image
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Steps

- Download a ubuntu image (Xenial)

```
wget http://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-disk1.img
```

- Install Guestfish

```
sudo apt-get install -y libguestfs-tools
```

- Open the ubuntu image

```
sudo guestfish --rw -a xenial-server-cloudimg-amd64-disk1.img
```

- Mount the ubuntu image

```
> run
> list-filesystems
> mount /dev/sda1 /
```

- Modify cloud.cfg

```
> vi /etc/cloud/cloud.cfg
```

```
# Line 12
Disable_root : false
Ssh_pwauth : true (add this line)

# Line 93
Lock_passwd : false
Plain_text_passwd : "ubuntu" (add this line)
```

```
> quit
```

