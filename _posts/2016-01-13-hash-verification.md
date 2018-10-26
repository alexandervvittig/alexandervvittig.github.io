---
id: 403
title: Hash verification 
date: 2016-01-13T23:19:10+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=403
permalink: /2016/01/13/hash-verification/
categories:
  - PowerShell
---
Another handy quick tip:
  
Ever needed to verify an ISO, to see if it has the right hash?
  
Super easy with Powershell!

<pre class="lang:ps decode:true">Get-FileHash -Path &lt;path&gt; -Algorithm MD5 | select hash</pre>

and you get the MD5 has as a result:

<pre class="lang:ps decode:true "># Will look something like this
Hash
----
C6DF6C9782B127FF277B03DC78FC7846</pre>

&nbsp;