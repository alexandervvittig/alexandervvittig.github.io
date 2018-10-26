---
id: 508
title: Run PowerShell Scripts from Task Scheduler
date: 2016-06-25T15:06:59+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=508
permalink: /2016/06/25/run-powershell-scripts-from-task-scheduler/
categories:
  - PowerShell
---
I assume that your are familiar with the Task Scheduler in Windows, so this one should be a quick one:

  1. Create a new task
  2. Create an Action
  3. Program/Script: <pre class="lang:default decode:true ">powershell.exe</pre>

  4. Add arguments: <pre class="lang:default decode:true ">-NoProfile -ExecutionPolicy Bypass C:\path_to_your_script.ps1</pre>

  5. Set all the other needed things liker any other scheduled task
  6.  Have an automated powershell script, easy right?