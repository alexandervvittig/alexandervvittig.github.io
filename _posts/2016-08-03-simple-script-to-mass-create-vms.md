---
id: 534
title: Simple script to mass create VMs
date: 2016-08-03T09:54:08+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=534
permalink: /2016/08/03/simple-script-to-mass-create-vms/
categories:
  - PowerShell
---
I am going to rebuild quite a few VMs in my lab with 2016 TP5 and nano servers and this will help speed up the process.

<pre class="lang:ps decode:true  ">$SRV1    = "2016_DC01"		                # Name of VM running Server Operating System
$SRAM    = 2GB				                # RAM assigned to Server Operating System
$SRV1VHD = 50GB				                # Size of Hard-Drive for Server Operating System
$VMLOC   = "D:\HyperV"			            # Location of the VM and VHDX files
$NetworkSwitch1 = "PrivateSwitch1"	        # Name of the Network Switch
$WSISO   = "C:\14300.1000.160324-1723.RS1_RELEASE_SVC_SERVER_OEMRET_X64FRE_EN-US.ISO"	        # Windows Server 2016 Technical Preview5 ISO
#$WSVFD   = "C:\autoattend\attendfile.vfd"	    # Windows Server 2008 Virtual Floppy Disk with autounattend.xml file

# Create VM Folder and Network Switch
mkdir $VMLOC -ErrorAction SilentlyContinue
$TestSwitch = Get-VMSwitch -Name $NetworkSwitch1 -ErrorAction SilentlyContinue; if ($TestSwitch.Count -EQ 0){New-VMSwitch -Name $NetworkSwitch1 -SwitchType Private}

# Create Virtual Machines
New-VM -Name $SRV1 -Path $VMLOC -MemoryStartupBytes $SRAM -NewVHDPath $VMLOC\$SRV1.vhdx -NewVHDSizeBytes $SRV1VHD -SwitchName $NetworkSwitch1

# Configure Virtual Machines
Set-VMDvdDrive -VMName $SRV1 -Path $WSISO
Set-VMFloppyDiskDrive -VMName $SRV1 -Path $WSVFD
Start-VM $SRV1
</pre>

&nbsp;