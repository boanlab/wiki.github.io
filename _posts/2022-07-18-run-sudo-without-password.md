---
title: Run sudo without Password
author: Jaehyun Nam
date: 2022-07-10
category: default
layout: post
---

## Configuration

```
sudo vi /etc/sudoers
```

```
# Allow all commands to run without a password
[USER_ID] ALL=NOPASSWD:ALL

# Allow only specific commands to run without a password
# (it also means that the user can't run the other commands with the root permission)
[USER_ID] ALL=NOPASSWD:cmd1,cmd2
```

