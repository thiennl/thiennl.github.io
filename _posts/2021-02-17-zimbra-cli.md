---
layout: post
title: "Zimbra Cli"
categories: system
tags: zimbra
---
<span style="color:green">*List tất cả tài khoản zimbra*</span>

```bash
#su - zimbra
$zmprov -l gaa
```
hoặc
```bash
#su - zimbra
$zmaccts | awk  '/@/{print $1}'
```
