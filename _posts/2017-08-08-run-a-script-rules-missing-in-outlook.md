---
id: 650
title: Run-a-Script Rules Missing in Outlook
date: 2017-08-08T16:03:48+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=650
permalink: /2017/08/08/run-a-script-rules-missing-in-outlook/
categories:
  - Break / Fix
---
Office 2016 and 2013 users who use run-a-script rules are discovering their scripts are currently disabled (as is Start Application), thanks to a security update. When the update is installed, any existing run-a-script and run application rules will be disabled.

<img class="size-full wp-image-651 alignleft" src="http://blog.vvittig.com/wp-content/uploads/2017/08/2017-08-08_15-55-59.jpg" alt="" width="224" height="56" />

&nbsp;

&nbsp;

&nbsp;

^ that option, &#8216;start application&#8217; is missing.

The fix is easy, as usual, just a registry key.  :o)

<pre class="lang:ps decode:true"># Outlook 2016
$registryPath = "HKCU:\Software\Microsoft\Office\16.0\Outlook\Security"
$Name = "EnableUnsafeClientMailRules"
$value = "1"
New-ItemProperty -Path $registryPath -Name $name -Value $value`
                 -PropertyType DWORD -Force -Verbose

# Outlook 2013
$registryPath = "HKCU:\Software\Microsoft\Office\15.0\Outlook\Security"
$Name = "EnableUnsafeClientMailRules"
$value = "1"
New-ItemProperty -Path $registryPath -Name $name -Value $value`
                 -PropertyType DWORD -Force -Verbose</pre>

Credit: [https://www.slipstick.com/outlook/rules/outlook-2016-run-a-script-rules](https://www.slipstick.com/outlook/rules/outlook-2016-run-a-script-rules/)

&nbsp;