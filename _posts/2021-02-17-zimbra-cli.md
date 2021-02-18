---
layout: post
title: "Zimbra Cli"
categories: system
tags: zimbra
---
**Zimbra Cli**
<span style="color:blue">*List tất cả tài khoản zimbra*</span>.

```bash
#su - zimbra
$zmprov -l gaa
```
hoặc
```bash
#su - zimbra
$zmaccts | awk  '/@/{print $1}'
```
