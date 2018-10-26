---
id: 672
title: 'So the Meltdown starts&#8230;'
date: 2018-01-04T13:02:07+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=672
permalink: /2018/01/04/so-the-meltdown-starts/
categories:
  - FYI
  - PowerShell
---
You probably have [heard](https://security.googleblog.com/2018/01/todays-cpu-vulnerability-what-you-need.html) or [read](https://www.theregister.co.uk/2018/01/02/intel_cpu_design_flaw/) about the current issues with chips and their vulnerability.

> A fundamental design flaw in Intel&#8217;s processor chips has forced a significant redesign of the Linux and Windows kernels to defang the chip-level security bug.

[CVE-2017-5754 (Meltdown) and CVE-2017-5715 (Spectre)](https://meltdownattack.com/)  are two nasty exploits and you might want to check your systems if they are patched.

Luckily the Microsoft Security Response Center has released a [PowerShell module named SpeculationControl](https://support.microsoft.com/en-us/help/4073119/windows-client-guidance-for-it-pros-to-protect-against-speculative-exe) which can be installed from the PowerShell Gallery.

<pre class="lang:ps decode:true ">Install-Module -Name SpeculationControl -Force

Get-SpeculationControlSettings

</pre>

[<img class="aligncenter size-full wp-image-674" src="http://blog.vvittig.com/wp-content/uploads/2018/01/meltdown.png" alt="" width="537" height="300" srcset="https://blog.vvittig.com/wp-content/uploads/2018/01/meltdown.png 537w, https://blog.vvittig.com/wp-content/uploads/2018/01/meltdown-300x168.png 300w" sizes="(max-width: 537px) 100vw, 537px" />](http://blog.vvittig.com/wp-content/uploads/2018/01/meltdown.png)

Additionally maybe look at [Mike&#8217;s post](http://mikefrobbins.com/2018/01/04/using-powershell-to-check-remote-windows-systems-for-cve-2017-5754-meltdown-and-cve-2017-5715-spectre/)

&nbsp;