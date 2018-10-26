---
id: 710
title: Edit Verbose Output of cmdlets
date: 2018-04-02T18:23:38+00:00
author: Alex W
layout: post
guid: https://blog.vvittig.com/?p=710
permalink: /2018/04/02/edit-verbose-output-of-cmdlets/
categories:
  - PowerShell
---
I wanted to append information to the verbose output of a cmdlet so that logging is neater. Well, it seems there is no nice way to do that?

This is what I came up with, redirecting the verbose stream, manipulating the verbose string, and then write it verbose back out

<pre class="lang:ps decode:true  ">$verbose_info = get-aduser awittig | set-aduser -Replace @{comment = 'test'} -Verbose 4&gt;&1
write-verbose "$(get-date) - $($verbose_info -split ':')" -Verbose

#Output
VERBOSE: 04/2/2018 16:35:01 - Performing the operation "Set" on target "CN=Wittig\, Alexander,OU=users,OU=test,DC=AD,DC=bloodyshell,DC=com".</pre>

Source: [https://blogs.technet.microsoft.com/heyscriptingguy/2014/03/30/understanding-streams-redirection-and&#8230;](https://blogs.technet.microsoft.com/heyscriptingguy/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell/)