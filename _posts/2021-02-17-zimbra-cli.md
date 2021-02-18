---
layout: post
title: "Zimbra Cli"
categories: system
tags: zimbra
---

**Zimbra Cli**


---
**List tất cả tài khoản zimbra**
```bash
#su - zimbra
$zmprov -l gaa
```

hoặc

```bash
#su - zimbra
$zmaccts | awk  '/@/{print $1}'
```
