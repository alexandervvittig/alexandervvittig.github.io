---
id: 660
title: Logon as batch job
date: 2017-11-13T16:17:17+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=660
permalink: /2017/11/13/logon-as-batch-job/
categories:
  - Uncategorized
---
If you are scheduling tasks, no doubt you run across the issue that if you need a task run as a different user, said user needs the right to logon as a batch job. Doing this is fairly easy:

  1. Start ****secpol.msc****
  2. Expand **Local Policies -> User Right Assignment**
  3. Find &#8220;Logon as a batch job&#8221;
  4. Add the user / service account as needed

This can of course also be set up via GPO.

  * Source: [Set Logon as batch job rights to User by Powershell,](http://www.morgantechspace.com/2014/03/Set-Logon-as-batch-job-rights-to-User-by-Powershell-CSharp-CMD.html) C# and CMD