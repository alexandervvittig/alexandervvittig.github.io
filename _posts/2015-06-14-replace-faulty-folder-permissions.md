---
id: 176
title: Replace faulty folder permissions
date: 2015-06-14T10:13:17+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=176
permalink: /2015/06/14/replace-faulty-folder-permissions/
categories:
  - Scripts
---
We were moving data with a tool called Syncedtool. It works pretty good, however the biggest downfall is, it does not copy NTFS permissions&#8230; UGG!

So here my Batch fix for it. Since PowerShell is a pain to be used to that&#8230;

<pre class="lang:ps decode:true ">::Since it has multiple folders I need to replace, I put it in a loop
:start
::subinACL installs in that folder and has to be used from there
cd C:\Program Files (x86)\Windows Resource Kits\Tools
set /p folder=Set the Data Path:
::First we clean out all permissions and get rid of the faulty ones
subinacl /subdirectories D:\users\%folder% /perm
subinacl /subdirectories D:\users\%folder% /grant=system=F
subinacl /subdirectories D:\users\%folder% /grant=&lt;user1&gt;=F
subinacl /subdirectories D:\users\%folder% /grant=administrators=F
subinacl /subdirectories D:\users\%folder% /grant="Domain Admin"=F
::Here we grant the user of the folder access to his folder
subinacl /subdirectories D:\users\%folder% /grant="&lt;domain&gt;\%folder%"=F
subinacl /subdirectories D:\users\%folder%\* /grant="everyone"=F
echo Finished for %folder%
goto start

</pre>

&nbsp;