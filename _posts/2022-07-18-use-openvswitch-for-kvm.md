---
title: Use Open vSwitch for KVM
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Configure Open vSwitch in KVM

- Check the list of KVM networks

    ```
    virsh net-list
    ```

- Edit the default network

    ```
    virsh net-edit default
    ```

    ```
    destroy the default network
    virsh net-destroy default
    ```

- Disable the autostart of the default network

    ```
    virsh net-autostart --disable default
    ```

- Make a new configuration for OpenvSwitch

    ```
    vi ovsbr0.xml
    ```

    ```
    <network>
        <name>ovsbr0
        <forward mode='bridge'/>
        <bridge name='ovsbr0'/>
        <virtualport type='openvswitch'/>
    </network>
    ```

- Add the new configuration into KVM networks

    ```
    virsh net-define ovsbr0.xml
    ```

- Start the new one

    ```
    virsh net-start ovsbr0
    ```

- Enable the autostart of the OpenvSwitch bridge

    ```
    virsh net-autostart ovsbr0
    ```

- Check the list of KVM networks

    ```
    virsh net-list
    ```

