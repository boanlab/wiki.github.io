---
title: Change the MAC address of a Network Interface
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Commands

```
vi /etc/udev/rules.d/75-mac-spoof.rules
```

```
ACTION=="add", SUBSYSTEM=="net", ATTR{address}=="XX:XX:XX:XX:XX:XX", RUN+="/usr/bin/ip link set dev %k address YY:YY:YY:YY:YY:YY"
```

