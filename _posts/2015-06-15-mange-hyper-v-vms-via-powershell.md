---
id: 183
title: Mange Hyper-V VMs via PowerShell
date: 2015-06-15T14:46:55+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=183
permalink: /2015/06/15/mange-hyper-v-vms-via-powershell/
categories:
  - Hyper-V
  - PowerShell
---
Some Hyper-V VM remote management commands:
  
For that to work right the VM has to be shut down.

Here a list of Hyper-V Commands<a href="https://technet.microsoft.com/en-us/library/hh848559(v=wps.630).aspx" target="_blank"><br /> https://technet.microsoft.com/en-us/library/hh848559(v=wps.630).aspx</a>

&#8211; Shut down VM

<pre class="lang:ps decode:true"># Get VMs on Host
Get-VM
# Shutdown VM - Forcefully
Stop-VM –VMname &lt;VmName&gt; -Force</pre>

&#8211; Set the amount of Cores assigned to the VM

<pre class="lang:ps decode:true "># Get all the VMs on the host
Get-VM
# Set the amount of assigned 
Set-VMProcessor -VMname &lt;VmName&gt; -Count 2 -Reserve 10 -Maximum 75 -RelativeWeight 200</pre>

&#8211; Set Amount of RAM assigned

<pre class="lang:ps decode:true"># Get VMs installed on host
Get-VM
# Assign RAM to VM
Set-VMMemory -VMname &lt;VmName&gt; -DynamicMemoryEnabled $true -MinimumBytes 64MB -StartupBytes 256MB -MaximumBytes 2GB -Priority 80 -Buffer 25</pre>

&#8211; Start VM back up

<pre class="lang:ps decode:true "># Start Virtual Machine
Start-VM -VMname &lt;VmName&gt;</pre>

&nbsp;