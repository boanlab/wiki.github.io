---
title: Disable LidSwitch on Ubuntu
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Configuration

```
sudo vi /etc/systemd/logind.conf
```

```
#HandleLidSwitch=suspend
HandleLidSwitch=ignore
```

```
sudo systemctl restart systemd-logind
```

