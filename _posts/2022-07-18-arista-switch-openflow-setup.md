---
title: Arista Switch OpenFlow Setup
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
EOS-4.12.7.1 (Serial speed: 9600)
```

## How to configure OpenFlow

- Default ID and password

    ```
    admin / [enter]
    ```

- Factory initialization

    ```
    # reload now
    (">" to "#" : enable)
    ```

- Write changes into the startup configuration

    ```
    # write memory
    # zerotouch cancel (if ZeroTouch is enabled)
    ```

- Set the IP address of the management port

    ```
    # configure terminal
    (config) # interface management 1
    (config-if) # ip address [switch IP]/24
    (config-if) # end
    ```

- Set the OpenFlow configuration

    ```
    # config
    (config) # openflow
    (config-openflow) # controller tcp:[controller IP]:[controller port]
    (config-openflow) # bind mode vlan
    (config-openflow) # bind vlan 1
    (config-openflow) # no shutdown
    (config-openflow) # keepalive
    ```

- Show the OpenFlow configuration

    ```
    # show openflow
    # show openflow flows
    # show openflow ports
    # show openflow profiles
    # show openflow queues
    # show openflow statistics
    ```

