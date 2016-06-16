---
layout: page
title: Submit a DNS Request
---

## Overview

## DNS Request

1. Go to the [DNS request form](http://urel-tech.wsu.edu/HelpDesk/DNSREQUEST.asp).
1. Enter your name and email address.
1. Enter the requested DNS change.
1. Click submit.

Example:
```
Request tacos.wsu.edu and www.tacos.wsu.edu to point to wsuwp-prod-01 (134.121.140.68)
```

You will receive an email notificate from the DNS help desk when your request has been approved or denied.

## Modify TTL Request

It's possible that the TTL (time to live) on a DNS record is set to something high like 86400 (24 hours). In these cases it can be helpful to first request that the TTL is lowered to 600 seconds so that when the DNS change is made it will propagate quickly.

## Check DNS records for a domain

### OSX / Linux

1. Open a command prompt.
1. Type `nslookup` and hit enter.
1. Type `set debug` and hit enter.
1. Type the domain name and hit enter.
1. Type `exit` and hit enter.

You should see a record for that domain that can help determine if a request has been applied yet.

```
› nslookup
> set debug
> web.wsu.edu
Server:		134.121.139.10
Address:	134.121.139.10#53

------------
    QUESTIONS:
	web.wsu.edu, type = A, class = IN
    ANSWERS:
    ->  web.wsu.edu
	internet address = 134.121.140.68
	ttl = 3600
    AUTHORITY RECORDS:
    ->  web.wsu.edu
	nameserver = ns1.wsu.edu.
	ttl = 3600
    ->  web.wsu.edu
	nameserver = ns2.wsu.edu.
	ttl = 3600
    ADDITIONAL RECORDS:
    ->  ns1.wsu.edu
	internet address = 134.121.139.10
	ttl = 86400
    ->  ns2.wsu.edu
	internet address = 134.121.80.36
	ttl = 86400
------------
Name:	web.wsu.edu
Address: 134.121.140.68
```
