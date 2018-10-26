---
id: 608
title: Get all cmdlets in a specific module
date: 2016-12-27T14:35:04+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=608
permalink: /2016/12/27/get-all-cmdlets-in-a-specific-module/
categories:
  - PowerShell
---
That might be old new for some of you, I was, however thrown off a little bit.

I installed a new Git module as I was playing with GitHub and wanted to update check for updates and update files accordingly. I am specifically talking about the [PowerShell Cheat Sheets](https://github.com/PrateekKumarSingh/CheatSheets), which is an awesome collection. Anywho after loading the module, I was a little stumped how to get the info of the cmdlets in the module. I tried

<pre class="lang:default decode:true ">help *git*</pre>

Which only resulted in 2-3 commands.

Well the answer is easy:

<pre class="lang:ps decode:true ">Get-Command -Module $module</pre>

This will give you all the cmdlets in a module. Pretty cool. :o)