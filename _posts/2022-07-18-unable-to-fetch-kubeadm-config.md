---
title: Unable to Fetch the kubeadm-config ConfigMap
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Message

```
sudo kubeadm join ...
```

```
... unable to fetch the kubeadm-config ConfigMap ...
```

- Change the old token to a new one

```
< master node >

$ kubeadm token create
[ new token ]

< compute node >

kubeadm join ... --token [ new token ] ...
```

