---
title: Port Forwarding using Socat
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Commands

- TCP Protocol

```
socat TCP-LISTEN:[port number],fork TCP:[target url or IP address]:[target port number]
```

- UDP Protocol

```
socat UDP-LISTEN:[port number],fork UDP:[target url or IP address]:[target port number]
```

