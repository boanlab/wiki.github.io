---
title: Pica8 Switch OpenFlow Setup
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
P-3290, P-3295, tested version: 2.3.7 (Serial speed: 19200)
```

## How to configure OpenFlow

- Change Mode

    ```
    sudo picos_boot

        select OVS
        type [switch IP]/24
        type [gateway IP]
    ```

- Start PicOS

    ```
    sudo service picos start
    ```

- Stop PicOS

    ```
    sudo service picos stop
    ```

- Restart PicOS

    ```
    sudo service pcios restart
    ```

- Setup OVS

    ```
    vi setup.sh
    ```

    ```
    #!/bin/bash
    ovs-vsctl del-br br0
    ovs-vsctl add-br br0 — set bridge br0 datapath_type=pica8
    ovs-vsctl set-fail-mode br0 secure
    ovs-vsctl set-controller br0 tcp:[controller IP]:[controller Port]
    ovs-vsctl — set bridge br0 protocols=OpenFlow10 (or OpenFlow13)
    for i in {1..48}
    do
        ovs-vsctl add-port br0 ge-1/1/$i vlan_mode=access tag=10 — set interface ge-1/1/$i type=pica8
        echo “$i is connected to bridge"
    done
    ```

    ```
    chmod +x setup.sh
    ./setup.sh
    ```

