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
---  
<span style="color:green">**@Check size account**</span>  
*get mailboz size = gms*  
```bash
[zimbra@mail ~]$ zmmailbox -z -m  thiennl@dinguyen.com gms
59.97 KB
```
---
<span style="color:green">**@Hiển thị mail trong inbox**</span>
*Hiển thị 4 messages mới nhất trong inbox* 
```bash
[zimbra@mail ~]$ zmmailbox -z -m thiennl@dinguyen.com s -t message -l 4 "in:inbox"
num: 4, more: false

     Id  Type   From                  Subject                                             Date
   ----  ----   --------------------  --------------------------------------------------  --------------
1.  342  mess   Nguyen                Fw: Linux Update: Manage Your Servers with Cockpit  02/19/21 11:27
2.  269  mess   Thien                 Test from hotmail                                   01/18/21 13:51
3.  268  mess   Nguyen                Test                                                01/18/21 13:35
4.  267  mess   Nguyen                Fw: Merry Christmas, Welcoming the New Year 2021    12/25/20 11:03
```  
