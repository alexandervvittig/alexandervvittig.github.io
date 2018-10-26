---
id: 216
title: I hate SQL and (bad!) vendor support
date: 2015-07-16T11:33:37+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=216
permalink: /2015/07/16/i-hate-sql-and-vendor-support/
categories:
  - Break / Fix
  - SQL
---
I was working with a vendor for some specialty software, they could install the software but were not able to configure SQL&#8230; though the software is heavily integrated with SQL.

I have to admit, I am not too familiar with SQL so troubleshooting it, I have to utilize my Google fu&#8230;

**Error:**

_&#8220;Error: Test connection to the database server has failed because of network problems:
  
\[DBNETLIB\]\[ConnectionOpen (Connect()).\]SQL Server does not exist or access denied.&#8221;_

**Fix:**

1. Login to the server -> Start -> All Programs -> Microsoft SQL Server -> Configuration Tools -> SQL Server Configuration Manager -> SQL Server Network Configuration -> Protocols for MSSQLSERVER -> right click “TCP/IP” and select “Enable”.

2. Start -> Run -> type “services.msc” -> Restart SQL service.

**PROTIP:**
  
Also check a service called &#8216;_SQL Server Browser_&#8216; and make sure it is running&#8230;

&nbsp;