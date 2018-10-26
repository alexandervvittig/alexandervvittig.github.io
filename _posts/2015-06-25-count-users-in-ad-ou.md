---
id: 190
title: Count Users in AD OU
date: 2015-06-25T09:19:26+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=190
permalink: /2015/06/25/count-users-in-ad-ou/
categories:
  - PowerShell
---
&nbsp;

For <a href="https://www.microsoft.com/en-us/Licensing/licensing-programs/spla-program.aspx" target="_blank">SPLA Licencing</a> , we have to report the amount of users we have in AD, which can be quite a pain, the more ADs and OUs are there.

With this one-liner you can get those numbers quicker.

<pre class="lang:ps decode:true">(Get-ADUser -Filter * -SearchBase "ou=&lt;OuName&gt;,dc=&lt;DomainName&gt;,dc=local").count</pre>

&nbsp;