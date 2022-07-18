---
title: Ctrl + Alt does not work in virt-manager
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Problem

```
when using virt-manager + X-Window on Mac OS, Ctrl + Alt doesn't work
```

## Solution

```
vi ~/.Xmodmap
```

```
clear Mod1 keycode 66 = Alt_L keycode 69 = Alt_R add Mod1 = Alt_L add Mod1 = Alt_R
```

