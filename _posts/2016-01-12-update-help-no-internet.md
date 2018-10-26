---
id: 401
title: Update help, no internet
date: 2016-01-12T23:18:55+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=401
permalink: /2016/01/12/update-help-no-internet/
categories:
  - PowerShell
---
We have quite a few systems that are for high security use and internal access only, which is fine however sometimes working on Powershell scripts using the help files would be quite, well , helpful.

What you can do however (starting Powershell v.3) is import and export export help files. Look at this:

<pre class="lang:ps decode:true "># Save Help Files for all modules
Save-Help -DestinationPath c:\PS_helpfiles -Module * -Force

# Copy the c:\pf_helpfiles to the server where you want to add them
Copy-Item -Path c:\ps_helpfiles -Destination \\server\c$\ps_helpfiles

# Update help from folder
Update-Help -SourcePath c:\ps_helpfiles -Module * -Force</pre>

&nbsp;