---
title: Change Permissions for WordPress
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## How to change permissions for WordPress

```
sudo chown -R www-data:www-data wp-content
```

```
sudo find . -type d -exec chmod 755 {} \;
sudo find . -type f -exec chmod 644 {} \;
```

