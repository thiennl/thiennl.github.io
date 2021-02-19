---
layout: post
title: "Zimbra Cli"
categories: system
tags: zimbra
---
<span style="color:green">**@List tất cả tài khoản zimbra**</span>
```bash
#su - zimbra
$zmprov -l gaa
```
hoặc
```bash
#su - zimbra
$zmaccts | awk  '/@/{print $1}'
```  
<span style="color:green">Check size account</span>  
---  
<span style="color:green">**@Check size account**</span>  
*get mailboz size = gms*  
```bash
[zimbra@mail ~]$ zmmailbox -z -m  thiennl@dinguyen.com gms
59.97 KB
```
