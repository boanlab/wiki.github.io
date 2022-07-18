---
title: Install and Run Pktgen-DPDK
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
# Tested on Ubuntu 16.04 / CentOS 7.2
```

## How to install Pktgen-DPDK

- Install Pktgen

    ```
    sudo apt-get install -y wget patch libpcap-dev (Ubuntu 16.04)
    yum install -y wget patch libpcap-devel (CentOS 7.2)

    curl -LO http://www.dpdk.org/browse/apps/pktgen-dpdk/snapshot/pktgen-3.5.0.tar.gz
    tar xvfz pktgen-3.5.0.tar.gz

    echo "export RTE_SDK=\$DPDK_DIR" >> ~/.bashrc
    echo "export RTE_TARGET=\$DPDK_TARGET" >> ~/.bashrc
    . ~/.bashrc

    cd pktgen-3.5.0
    make
    ```

- Run Pktgen

    ```
    cd pktgen-3.5.0
    sudo -E app/$RTE_TARGET/pktgen -c 0xf -n 4 -- -p 0x3 -P -m "[1:2].0, [3:4].1"
        => [1:2].0 : use core #1 and #2 for port 0
        => [3:4].1 : use core #3 and #4 for port 1
    ```

    ```
    Pktgen:/> set [port number] [parameter] [value]

    set 0 count 100
        => send 100 packets to port 0

    set 0 size 64
        => send 64-byte packets to port 0

    set 0 rate 50
        => send packets to port 0 with 50% sending rate

    set 0 src ip 10.0.0.0/24
        => configure a source IP address

    set 0 src mac aa:bb:cc:dd:ee:ff
        => configure a source MAC address

    start 0
        => start to send packets

    stop 0
        => stop sending packets
    ```

