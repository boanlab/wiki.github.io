---
title: HP Switch OpenFlow Setup
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
HP-3800 J9575A (Serial speed: 9600)
```

## How to configure OpenFlow

- Connect the console of a switch

    ```
    # erase all -> Clean up everything
    # menu
    ```

    ```
    Select - 2 Switch Configuration...
    Select - 5 IP Configuration

    Choose - [ Edit ]
    Type - Gateway -> [gateway IP]
    Change - DHCP/Bootp -> Manual
    Type - [IP Address] / [Subnet Mask]
    Choose - [ Save ]

    Select - 0 Return to Main Menu...
    Select - 3 Console Passwords...
    Select - 3 Delete Password Pretection

    Change - [ No ] -> [ Yes ]

    Select - 1 Set Operator Password
    Select - 2 Set Manager Password
    Select - 0 Return to Main Menu...
    Select - 8 Run Setup

    Choose - [ Save ]
    ```

- Connect the switch IP using a web browser

    ```
    # username could be either "manager" or "operator"
    # login as "manager"
    ```

    ```
    Select - VLAN -> VLAN Mgmt

    Click - [Add VLAN]

    Type - ID: 10
    Type - VLAN Name: vlan_of

    Click - [Save]

    Choose - vlan_of

    Click - Ports -> [Change]
    Pick - specific ports or port range that you want to use as data plane ports managed by OpenFlow
    Choose - "untagged"

    Click - [Save]
    ```

- Connect the console again

    ```
    # config
    (config) # openflow
    (openflow) # controller-id 1 ip [controller IP #1] controller-interface vlan 1
    (openflow) # controller-id 2 ip [controller IP #2] controller-interface vlan 1
    (openflow) # controller-id 3 ip [controller IP #3] controller-interface vlan 1
    ```

- In the case of HP, it only allows users to add three controller IPs

    ```
    (openflow) # instance oflow
    (of-inst-oflow) # member vlan 10
    (of-inst-oflow) # controller-id 1
    (of-inst-oflow) # controller-id 2
    (of-inst-oflow) # controller-id 3
    (of-inst-oflow) # version 1.0 (or 1.3) -> OpenFlow 1.3 is not working well
    (of-inst-oflow) # enable
    (of-inst-oflow) # exit
    (openflow) # enable
    ```

- Check the configuration of OpenFlow

    ```
    (openflow) # show openflow controllers
    (openflow) # show openflow instance oflow
    ```

