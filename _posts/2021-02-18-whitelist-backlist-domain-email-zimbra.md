---
layout: post
title: "Whitelist/blacklist domain, email zimbra"
categories: system
tags: zimbra
author: thiennl
---



-- Black mail specific word in body or attachment

```
body     LOCAL_RULE1     /Danh sach ung vien Ban Chap Hanh/i
score    LOCAL_RULE1     10.0
```

---
-- Whitelist/blacklist domain, email


C1/ Test OK: Sử dụng file 
```
/opt/zimbra/conf/amavisd.conf.in
```
--> Gán điểm cho domain, email:
	+  = blacklist
	-  = whitelist
1. Whitelist domain dinguyen.com :  thêm  'dinguyen.com'                                  => -10.0,
```
#su - zimbra
$vi /opt/zimbra/conf/amavisd.conf.in
    #  read_hash("/var/amavis/sender_scores_sitewide"),
       { # a hash-type lookup table (associative array)
         'nobody@cert.org'                          => -3.0,
         'cert-advisory@us-cert.gov'                => -3.0,
         'owner-alert@iss.net'                      => -3.0,
         'slashdot@slashdot.org'                    => -3.0,
         'securityfocus.com'                        => -3.0,
         'dinguyen.com'                             => -10.0,
         'ntbugtraq@listserv.ntbugtraq.com'         => -3.0
$zmamavisdctl restart
```
Check log:  tail -f /var/log/zimbra.log | grep thiennl@dinguyen.com
 Passed CLEAN {RelayedInbound},
[zimbra@mta1 conf]$ tail -f /var/log/zimbra.log | grep thiennl@dinguyen.com
```
Jan 21 11:26:20 mta1 postfix/smtpd[25980]: NOQUEUE: filter: RCPT from unknown[123.31.35.57]: <thiennl@dinguyen.com>: Sender address triggers FILTER smtp-amavis:[127.0.0.1]:10026; from=<thiennl@dinguyen.com> to=<testmail@cpc.vn> proto=ESMTP helo=<gw-fmvnpt2018.vnptdata.vn>
Jan 21 11:26:20 mta1 postfix/smtpd[25980]: NOQUEUE: filter: RCPT from unknown[123.31.35.57]: <thiennl@dinguyen.com>: Sender address triggers FILTER smtp-amavis:[127.0.0.1]:10024; from=<thiennl@dinguyen.com> to=<testmail@cpc.vn> proto=ESMTP helo=<gw-fmvnpt2018.vnptdata.vn>
Jan 21 11:26:21 mta1 postfix/qmgr[5742]: 10B7218ED12A: from=<thiennl@dinguyen.com>, size=3310, nrcpt=1 (queue active)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) ESMTP [127.0.0.1]:10024 /opt/zimbra/data/amavisd/tmp/amavis-20210121T112553-30688-sTUE8isY: <thiennl@dinguyen.com> -> <testmail@cpc.vn> SIZE=3310 Received: from mta1.cpc.vn ([127.0.0.1]) by localhost (mta1.cpc.vn [127.0.0.1]) (amavisd-new, port 10024) with ESMTP for <testmail@cpc.vn>; Thu, 21 Jan 2021 11:26:21 +0700 (+07)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) Checking: HnYFfPf-vHfk [123.31.35.57] <thiennl@dinguyen.com> -> <testmail@cpc.vn>
Jan 21 11:26:21 mta1 postfix/qmgr[5742]: 88C4C18ED12D: from=<thiennl@dinguyen.com>, size=3995, nrcpt=1 (queue active)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) HnYFfPf-vHfk FWD from <thiennl@dinguyen.com> -> <testmail@cpc.vn>, BODY=7BIT 250 2.0.0 from MTA(smtp:[127.0.0.1]:10025): 250 2.0.0 Ok: queued as 88C4C18ED12D
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) Passed CLEAN {RelayedInbound}, [123.31.35.57]:48460 [123.31.35.57] <thiennl@dinguyen.com> -> <testmail@cpc.vn>, Queue-ID: 10B7218ED12A, Message-ID: <c38a24426fe64ec38d74d9b5b643b624@vnpt.vn>, mail_id: HnYFfPf-vHfk, Hits: 1.249, size: 3310, queued_as: 88C4C18ED12D, 478 ms
```

2. Blacklist domain dinguyen.com:   'dinguyen.com'                                  => 10.0,
```
#su - zimbra
$vi /opt/zimbra/conf/amavisd.conf.in
    #  read_hash("/var/amavis/sender_scores_sitewide"),
       { # a hash-type lookup table (associative array)
         'nobody@cert.org'                          => -3.0,
         'cert-advisory@us-cert.gov'                => -3.0,
         'owner-alert@iss.net'                      => -3.0,
         'slashdot@slashdot.org'                    => -3.0,
         'securityfocus.com'                        => -3.0,
         'dinguyen.com'                                  => -10.0,
         'ntbugtraq@listserv.ntbugtraq.com'         => -3.0
$zmamavisdctl restart
```
Check log:  tail -f /var/log/zimbra.log | grep thiennl@dinguyen.com
Passed SPAMMY {RelayedTaggedInbound}
```
[zimbra@mta1 conf]$ tail -f /var/log/zimbra.log | grep thiennl@dinguyen.com
Jan 21 11:26:20 mta1 postfix/smtpd[25980]: NOQUEUE: filter: RCPT from unknown[123.31.35.57]: <thiennl@dinguyen.com>: Sender address triggers FILTER smtp-amavis:[127.0.0.1]:10026; from=<thiennl@dinguyen.com> to=<testmail@cpc.vn> proto=ESMTP helo=<gw-fmvnpt2018.vnptdata.vn>
Jan 21 11:26:20 mta1 postfix/smtpd[25980]: NOQUEUE: filter: RCPT from unknown[123.31.35.57]: <thiennl@dinguyen.com>: Sender address triggers FILTER smtp-amavis:[127.0.0.1]:10024; from=<thiennl@dinguyen.com> to=<testmail@cpc.vn> proto=ESMTP helo=<gw-fmvnpt2018.vnptdata.vn>
Jan 21 11:26:21 mta1 postfix/qmgr[5742]: 10B7218ED12A: from=<thiennl@dinguyen.com>, size=3310, nrcpt=1 (queue active)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) ESMTP [127.0.0.1]:10024 /opt/zimbra/data/amavisd/tmp/amavis-20210121T112553-30688-sTUE8isY: <thiennl@dinguyen.com> -> <testmail@cpc.vn> SIZE=3310 Received: from mta1.cpc.vn ([127.0.0.1]) by localhost (mta1.cpc.vn [127.0.0.1]) (amavisd-new, port 10024) with ESMTP for <testmail@cpc.vn>; Thu, 21 Jan 2021 11:26:21 +0700 (+07)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) Checking: HnYFfPf-vHfk [123.31.35.57] <thiennl@dinguyen.com> -> <testmail@cpc.vn>
Jan 21 11:26:21 mta1 postfix/qmgr[5742]: 88C4C18ED12D: from=<thiennl@dinguyen.com>, size=3995, nrcpt=1 (queue active)
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) HnYFfPf-vHfk FWD from <thiennl@dinguyen.com> -> <testmail@cpc.vn>, BODY=7BIT 250 2.0.0 from MTA(smtp:[127.0.0.1]:10025): 250 2.0.0 Ok: queued as 88C4C18ED12D
Jan 21 11:26:21 mta1 amavis[30688]: (30688-02) Passed CLEAN {RelayedInbound}, [123.31.35.57]:48460 [123.31.35.57] <thiennl@dinguyen.com> -> <testmail@cpc.vn>, Queue-ID: 10B7218ED12A, Message-ID: <c38a24426fe64ec38d74d9b5b643b624@vnpt.vn>, mail_id: HnYFfPf-vHfk, Hits: 1.249, size: 3310, queued_as: 88C4C18ED12D, 478 ms
```
