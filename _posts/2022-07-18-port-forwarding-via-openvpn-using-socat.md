---
title: Port Forwarding via OpenVPN using Socat
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Commands

```
sudo apt-get install -y openvpn socat
```

```
sudo mkdir /etc/openvpn/[name]
sudo vi /etc/openvpn/[name]/[name].ovpn
```

```
... OpenVPN Configuration ...
auth-user-pass /etc/openvpn/[name]/[name].auth
... OpenVPN Configuration ...
```

```
sudo touch /etc/openvpn/[name]/[name].auth
```

```
[ID]
[PASSWORD]
```

```
sudo vi /etc/systemd/system/[name]-vpn.service
```

```
[Unit]
Description=OpenVPN Client Service
After=multi-user.target

[Service]
Type=idle
ExecStart=/usr/sbin/openvpn --config /etc/openvpn/[name]/[name].ovpn

[Install]
WantedBy=multi-user.target
```

```
sudo systemctl enable [name]-vpn.service
sudo vi /etc/init.d/socat
```

```
#!/bin/bash

SOCAT=/usr/bin/socat
PIDFILE=/var/run/socat.pid
LOGFILE=/var/log/socat.log
TARGET=[Internal Target Server IP Address]

start() {
    $SOCAT TCP-LISTEN:80,fork TCP:$TARGET:80 < /dev/null > $LOGFILE &
    $SOCAT TCP-LISTEN:443,fork TCP:$TARGET:443 < /dev/null > $LOGFILE &
    echo $! > $PIDFILE
}

stop() {
    /bin/kill $(/bin/cat $PIDFILE)
}

restart() {
    stop
    start
}

case "$1" in
    start)
        start;;
    stop)
        stop;;
    restart)
        restart;;
    *)
        echo "Usage: $0 {start|stop|restart}"
        exit 1
esac

exit $?
```

```
sudo chmod +x /etc/init.d/socat
sudo update-rc.d socat defaults
```

