---
title: Redirect Web Pages according to Domain Names
author: Jaehyun Nam
date: 2022-07-10
category: default
layout: post
---

## PHP Code

```
<?php
    if ($_SERVER['HTTP_HOST'] == "abc.domain.com") {
        echo "<meta http-equiv='refresh' content='0;url=http://abc.domain.com'></meta>";
    } else {
        echo "<meta http-equiv='refresh' content='0;url=http://def.domain.com'></meta>";
    }
?>
```

