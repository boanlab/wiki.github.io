---
title: Change the timeout of GRUB
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Configuration

```
sudo vi /boot/grub/grub.cfg
```

```
replace "set timeout=x" to "set timeout=y"

x = the original value
y = the value that you want to set
```

