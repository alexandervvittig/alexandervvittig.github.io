---
id: 396
title: Find your VHDs in Hyper-V
date: 2016-01-10T17:31:55+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=396
permalink: /2016/01/10/find-your-vhds-in-hyper-v/
categories:
  - Hyper-V
  - PowerShell
---
A virtual machine in Hyper-V consists of a few files that account for its virtual hardware configuration and the virtual storage (VHD and VHDX files).  By default the virtual machine configuration files are stored in_C:\ProgramData\Microsoft\Windows\Hyper-V_, and the virtual hard drives are stored in _C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks_.

One slight improvement in Hyper-V (in Windows Server 2012) is that during the installation process (GUI mode only) it gives you the option of changing these defaults.  However the defaults are still the same as they used to be… on the C drive.

Being cheap I only have a &#8216;tiny&#8217; SSD (ok folks I bought it years ago and it felt like it was a fortune back then&#8230;) as C:\, all other data is still on rusty spindles on my home lab.

VMs, I know are important but are small are still on the C:\ however others I had to move off.

Now tiering storage is fine, it is a PITA to find where which VHD/VHDX is stored via GUI. The fastest way I found to scavenger your lost treas&#8230; um VHDs is of course Powershell.

<pre class="lang:ps decode:true "># Run as admin
Get-VMHardDiskDrive * | Select VMName, Path</pre>

then being a little OCD&#8230;, I like to sort it after names. An example can look like this:

<pre class="lang:ps decode:true  ">PS C:\WINDOWS\system32&gt; Get-VMHardDiskDrive * | select vmname, path | Sort-Object VMName

VMName    Path
------    ----
2016      E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\2016.vhdx
CentOS_01 C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\CentOS_01.vhdx
CentOS_02 C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\CentOS_02.vhdx
CentOS_03 C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\CentOS_03.vhdx
CentOS_04 C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\CentOS_04.vhdx
DC01      E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\DC01.vhdx
DC02      E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\DC02.vhdx
Kali      E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\Kali.vhdx
SCCM01    E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\SCCM01.vhdx
SCCM02    C:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\SCCM02.vhdx
SpiceW    E:\Users\Public\Documents\Hyper-V\Virtual Hard Disks\SpiceW.vhdx</pre>

Now, that is not bad, what if I need more info, let&#8217;s say also the VMID so you can quickly RDP into the VM (<a href="http://blog.vvittig.com/2015/12/30/rdcman-to-hyper-v-console/" target="_blank">see my post about RDCMan</a>).

Easy, **Get-VMHardDiskDrive** does not have the info about the VMID, **Get-VM** however does, so we can just pipe that in it like so:

<pre class="lang:ps decode:true ">Get-VM * | Get-VMHardDiskDrive | Select vmname,vmid,path | Sort-Object vmname</pre>

That will give us a nice list with the VMname, VMID and VHD(x) path.

Another thing to mention. if you wan to change the default location of your VM Disks, or even of the machines, Powershell can do that as well:

<pre class="lang:ps decode:true ">SET-VMHOST –computername &lt;server&gt; –virtualharddiskpath 'C:\VHDs'
SET-VMHOST –computername &lt;server&gt; –virtualmachinepath 'C:\VMs'</pre>

or via GUI of course in the Hyper-V settings:

<a href="http://blog.vvittig.com/wp-content/uploads/2016/01/2016-01-10_17-31-06.png" rel="attachment wp-att-399"><img class="aligncenter size-full wp-image-399" src="http://blog.vvittig.com/wp-content/uploads/2016/01/2016-01-10_17-31-06.png" alt="2016-01-10_17-31-06" width="254" height="112" /></a>