---
title: Reset GitLab Root Password (Docker)
author: Jaehyun Nam
date: 2022-07-18
category: default
layout: post
---

## Commands

```
docker exec -it [gitlab container ID] bash
```

```
gitlab-rails console -e production
```

```
irb(main):001:0> user = User.where(id:1).first
irb(main):002:0> user.password = 'PASSWORD'
irb(main):003:0> user.password_confirmation = 'PASSWORD'
irb(main):004:0> user.save!
```

