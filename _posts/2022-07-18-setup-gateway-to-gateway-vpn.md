---
title: Set Up Gateway-to-Gateway VPN
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## VPN setup script

```
#!/bin/bash
# https://wiki.debian.org/IPsec

if [ "$#" -ne 5 ];
then
    echo "Usage: $0 [local public ip] [local virtual ip] [remote public ip] [remote virtual ip]"
    exit 1
fi

echo "install packages..."

sudo apt-get install -y ipsec-tools racoon

calc_mask () {
    local ip=$1
    var=$(echo $ip | awk -F"." '{print $1,$2,$3,$4}')
    set -- $var
    ip="$1.$2.$3.0"
    echo "$ip"
}

loc_pip=$1
loc_vip=$2
rmt_pip=$3
rmt_vip=$4
shared_key=$5

echo "create configurations..."

echo "\
path pre_shared_key \"/etc/racoon/psk.txt\";
remote $rmt_pip
{
    exchange_mode aggressive, main;
    proposal {
        encryption_algorithm 3des;
        hash_algorithm sha1;
        authentication_method pre_shared_key;
        dh_group 2;
    }
}

sainfo address $(calc_mask $loc_vip)/24 any address $(calc_mask $rmt_vip)/24 any
{
    pfs_group 2;
    lifetime time 24 hour;
    encryption_algorithm 3des, blowfish 448, rijndael;
    authentication_algorithm hmac_sha1, hmac_md5;
    compression_algorithm deflate;
}" | sudo tee /etc/racoon/racoon.conf

echo "\
$rmt_pip  $shared_key
" | sudo tee /etc/racoon/psk.txt
echo "\
flush;
spdflush;
spdadd $(calc_mask $loc_vip)/24 $(calc_mask $rmt_vip)/24 any -P out ipsec
esp/tunnel/$loc_pip-$rmt_pip/require;
spdadd $(calc_mask $rmt_vip)/24 $(calc_mask $loc_vip)/24 any -P in ipsec
esp/tunnel/$rmt_pip-$loc_pip/require;
" | sudo tee /etc/ipsec-tools.conf

echo "restart services..."

sudo /etc/init.d/setkey restart
sudo /etc/init.d/racoon restart

echo "set environments..."

sudo route del -net $(calc_mask $rmt_vip) netmask 255.255.255.0
sudo ip route add to $(calc_mask $rmt_vip)/24 via $loc_pip src $loc_vip
echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward

echo "done."
```

## VPN restart script

```
#!/bin/bash

sudo /etc/init.d/setkey restart
sudo /etc/init.d/racoon restart
```

