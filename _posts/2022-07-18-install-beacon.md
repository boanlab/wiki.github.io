---
title: Install Beacon
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
# Tested on Ubuntu 18.04
# Beacon version: v1.0.4
```

## How to install Beacon

```
sudo apt-get -y install openjdk-8-jre openjdk-8-jdk
wget https://boanlab.com/downloads/sdn/beacon-1.0.4-linux_x86_64.tar.gz
tar -zxvf beacon-1.0.4-linux_x86_64.tar.gz -C ~
```

## How to run Beacon

```
cd ~/beacon-1.0.4
sed -i "s/#controller.threadCount=1/controller.threadCount=$(nproc)/g" beacon.properties
./beacon -configuration configurationSwitch
```

