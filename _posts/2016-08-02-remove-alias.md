---
id: 531
title: Remove alias
date: 2016-08-02T21:32:11+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=531
permalink: /2016/08/02/remove-alias/
categories:
  - Uncategorized
---
PowerShell is very structured, but there are exception, removing an alias is one of many.

<pre class="lang:ps decode:true "># Create a new alias
New-Alias -Name Test -Value TestValue
# Check if the alias was created
Get-Alias Test
# Remove that sucker
# Naturally in PowerShell you'd think it is remove-alias, but it is not
Remove-Item alias:Test</pre>

&nbsp;