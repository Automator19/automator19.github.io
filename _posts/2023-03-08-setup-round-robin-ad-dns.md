---
layout: post
title: How to setup round robin on AD DNS ?
category: [Windows]
---

# What is round robin ?
- Round robin DNS is mathoed is used to load balance request between a number of servers. 

- It works from a list of IP addresses on rotation basis. 

- First request will be forwarded to the first IP
Second reqest will be forewarded to the second IP and so on. 

- Every time IP is handed out it moved to the end of the list. 

# How to setup round robin on AD DNS ?

- Windows supports round robin when IP is assigned to multiple DNS names - e.g ftp.domain.com or smtp.domain.com

- First check RR is enabled at DNS level - Right Click DNS Server --> Properties --> Advanced --> Make sure RR is ticked

- Add Multiple A Records 

- Enable Advanced option from view 

- Open first A record and change the TTL value - This is amount of time it will response to any client before switching to another IP 

- For round robin we need to set TTL to 0. Meaning first DNS lookup first IP will respond, Second DNS lookup second IP will respond