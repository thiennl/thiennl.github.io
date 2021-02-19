---
layout: post
title: "Quản lý mailbox zimbra sử dụng cli"
categories: system
tags: zimbra
---
<span style="color:green">*List tất cả folder*</span>  
$zmmailbox -z -m user@example.net getAllFolders<br>
$zmmailbox -z -m user@example.net gaf  
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

