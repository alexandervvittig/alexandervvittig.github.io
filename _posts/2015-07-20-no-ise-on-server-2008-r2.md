---
id: 236
title: No ISE on Server 2008 R2
date: 2015-07-20T13:29:11+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=236
permalink: /2015/07/20/no-ise-on-server-2008-r2/
categories:
  - PowerShell
---
I was working today on a 2008 R2 machine and wanted to write a script and was compuzzled where there was no PowerShell ISE on that server?! Come to find out that the ISE is not installed by default on 2008 R2. Grr&#8230;

Here how to install it with a 2 liner: (run PS as admin)

<pre class="lang:ps decode:true ">Import-Module ServerManager
# In newer PS versions just 'install-windowsfeature'
Add-Windowsfeature PowerShell-ISE
</pre>

&nbsp;