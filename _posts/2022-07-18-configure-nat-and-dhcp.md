---
title: Configure NAT and DHCP
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Network Setup

```
sudo vi /etc/network/interfaces
```

```
auto lo
iface lo net loopback

auto eth0 # External network
iface eth0 inet dhcp

auto eth1 # Internal network
iface eth1 inet static
    address 192.168.0.1
    network 192.168.0.0
    netmask 255.255.255.0
    broadcast 192.168.0.255
```

```
sudo /etc/init.d/networking restart
```

## Masquerade Setup

```
sudo vi /etc/sysctl.conf
```

```
uncomment "net.ipv4_ip_forward=1"
```

```
sudo vi /etc/rc.local
```

```
/sbin/iptables -P FORWARD ACCEPT
/sbin/iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

## DHCP Setup

```
sudo apt-get install -y isc-dhcp-server
sudo vi /etc/dhcp/dhcpd.conf
```

```
ddns-update-style none;
option domain-name "localhost";
option domain-name-servers 8.8.8.8;
default-lease-time 3600;
max-lease-time 7200;
authoritative;
log-facility local7;

subnet 192.168.0.0 netmask 255.255.255.0 {
    range 192.168.0.2 192.168.0.254;
    option subnet-mask 255.255.255.0;
    option routers 192.168.0.1;
}
```

```
sudo vi /etc/default/isc-dhcp-server
```

```
INTERFACES="eth1"
```

```
sudo service isc-dhcp-server restart
```

