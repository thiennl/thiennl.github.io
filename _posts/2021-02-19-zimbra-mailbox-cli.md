---
layout: post
title: "Quản lý mailbox zimbra sử dụng cli"
categories: system
tags: zimbra
---
<span style="color:green">**@List tất cả folder**</span>
```bash  
$zmmailbox -z -m user@example.net getAllFolders  
hoặc  
$zmmailbox -z -m user@example.net gaf
```
```bash
[zimbra@mail ~]$ zmmailbox -z -m thiennl@dinguyen.com getAllFolders
        Id  View      Unread   Msg Count  Path
----------  ----  ----------  ----------  ----------
         1  unkn           0           0  /
        16  docu           0           0  /Briefcase
        10  appo           0           0  /Calendar
        14  mess           0           0  /Chats
         7  cont           0           0  /Contacts
         6  mess           0           1  /Drafts
        13  cont           0           4  /Emailed Contacts
         2  mess           1           4  /Inbox
         4  mess           0           0  /Junk
         5  mess           0           6  /Sent
        15  task           0           0  /Tasks
         3  unkn           0           0  /Trash
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
*Hiển thị 3 messages mới nhất trong sent*  
```bash
[zimbra@mail ~]$ zmmailbox -z -m thiennl@dinguyen.com s -t message -l 3 "in:sent"
num: 3, more: true

     Id  Type   From                  Subject                                             Date
   ----  ----   --------------------  --------------------------------------------------  --------------
1.  340  mess   Thien                 Hello Yahoo 1                                       02/19/21 11:26
2.  323  mess   Thien                 Testmail                                            02/03/21 08:44
3.  321  mess   Thien                    TEST MAIL                                           12/23/20 16:42
```  