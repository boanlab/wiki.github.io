---
title: Install Ryu
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Test Environment

```
# Tested on Ubuntu 18.04
# Ryu version: v4.34
```

## How to install Ryu

```
sudo apt-get -y install build-essential python-dev python-pip libffi-dev libssl-dev libxml2-dev libxslt1-dev zlib1g-dev
```

```
git clone https://github.com/faucetsdn/ryu.git
cd ryu; git checkout v4.34
pip install .
```

## How to run Ryu

- Execute RYU with the simple with for OpenFlow 1.0

    ```
    ./bin/ryu-manager --verbose ryu.app.simple_switch
    ```

- Execute RYU with the simple with for OpenFlow 1.3

    ```
    $ ./bin/ryu-manager --verbose ryu.app.simple_switch_13
    ```

## Troubleshooting

- Case 1

    ```
    File "/home/namjh/.local/lib/python2.7/site-packages/tinyrpc/protocols/__init__.py", line 15
        def __init__(self) -> None:
    ```

    ```
    pip uninstall tinyrpc
    pip install tinyrpc==0.8
    ```

- Case 2

    ```
    File "/home/namjh/.local/lib/python2.7/site-packages/ryu/app/wsgi.py", line 111, in _AlreadyHandledResponse
        from eventlet.wsgi import ALREADY_HANDLED
    ImportError: cannot import name ALREADY_HANDLED
    ```

    ```
    pip uninstall eventlet
    pip install eventlet==0.30.2
    ```

