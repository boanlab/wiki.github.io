---
title: Enable TCP Port for External Connection to Docker
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Configure docker.service

```
sudo vi /lib/systemd/system/docker.service
```

```
ExecStart=/usr/bin/dockerd -H fd:// -H tcp://0.0.0.0:2375
```

## Restart docker.service

```
sudo systemctl daemon-reload
sudo service docker restart
```

