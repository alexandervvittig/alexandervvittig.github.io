---
id: 192
title: Mass change logon script in AD
date: 2015-07-01T16:53:42+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=192
permalink: /2015/07/01/mass-change-logon-script-in-ad/
categories:
  - Active Directory
  - PowerShell
---
We needed to change login scripts, or rather remove &#8217;em as we replace &#8217;em with GPOs. I exported the current scripts to a TXT and then just cleared the field in AD.

<pre class="lang:ps decode:true ">#  Load the AD module
Import-module ActiveDirectory 
#  Get all the AD user who have a login script and save it to a textfile
Get-ADUser -filter * -properties scriptpath | ft Name, scriptpath &gt; C:\LogonScript.txt -Force
#  Clear the Logon script field in AD
Get-ADUser -Filter * -SearchBase "OU=TEST,DC=TEST,DC=local" | Set-ADUser -Clear scriptPath</pre>

&nbsp;