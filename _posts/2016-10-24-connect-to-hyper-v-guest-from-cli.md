---
id: 583
title: Connect to Hyper-V guest from CLI
date: 2016-10-24T14:46:35+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=583
permalink: /2016/10/24/connect-to-hyper-v-guest-from-cli/
categories:
  - PowerShell
---
One thing that has annoyed me for a long time, si the fact that there was no obvious / easy way to connect to the console session of a VM, so you have to open the Hyper-V manager, click on your VM and click on &#8216;connect&#8217;. That&#8217;s just too much clicking&#8230;

<pre class="lang:ps decode:true ">function enter-vmsession{
  [cmdletbinding()]
  param($vmhost=$env:computername,$vmname)
  vmconnect.exe $vmhost $vmname
}</pre>

I found that Hyper-V manager is using the &#8216;vmconnect.exe&#8217; to connect to the console session, and I wrote this little function that will kind of act like &#8216;enter-pssession&#8217; just instead of connection to a session it actually launches the vm console. Saved me alot of time. :o)