---
layout: post
title: "Tạo/xóa account zimbra theo danh sách"
categories: system
tags: zimbra
author: thiennl
---
<span style="color:green">**1. Tạo account/user theo danh sách**</span>
B1: Login zimbra account
```bash
#su – zimbra
```
B2: Tạo file bulk các accout cần tạo
```bash
$vi email.zmp
ca di1@dinguyen.com password123 displayName 'Di Nguyen 1' givenName Di sn Nguyen 
ca di2@dinguyen.com password456 displayName 'Di Nguyen 2' givenName Di sn Nguyen
```
B3: Run file bulk để tạo các account
```bash
$zmprov –f email.zmp
```
---
<span style="color:green">**1. Xóa account/user theo danh sách**</span>
B1: Login zimbra account
```bash
#su – zimbra
```
B2: Tạo file bulk các accout cần xóa
```bash
$vi email.zmp
da di1@dinguyen.com
da di2@dinguyen.com
```
B3: Run file bulk để xóa các account
```bash
$zmprov –f email.zmp
```