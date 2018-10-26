---
id: 568
title: Installing Nano Server
date: 2016-10-14T18:53:36+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=568
permalink: /2016/10/14/installing-nano-server/
categories:
  - Hyper-V
  - PowerShell
---
By now, I&#8217;m sure everyone has heard of Nano server, it is the next big or rather small thing form Microsoft. If you just started you looking into Nano server, the process is quite confusing, as it is well not a standalone server, but more like a self build mini server version.

Here my script how to build one from scratch, super easy.

<pre class="lang:ps decode:true  "># Prerequisites:
# Download the latest server 2016 ISO
# Copy the $drive\'NanoServer' folder to a local resource

# Set the location of the localrsource and point to the NanoServerImageGenerator folder
Set-Location 'D:\NanoServer\NanoServerImageGenerator'
# Import the NanoServerImageGenerator module
Import-Module .\NanoServerImageGenerator.psd1 -Verbose
# Define the local machine password for the NanoServer
$nano_admin_password = ConvertTo-SecureString -AsPlainText -Force -String 'Pa$$word#123'
# Define the server's name
$nano_servername = ("nano" + "_" + (Get-Date).month + (Get-Date).day)
# Create the server vhd with the following settings
New-NanoServerImage -MediaPath D:\ -BasePath .\Base -TargetPath ".\$($nano_servername).vhd" `
                    -DeploymentType Guest -Edition Datacenter -Storage -Defender `
                    -EnableRemoteManagementPort -ComputerName $nano_servername `
                    -AdministratorPassword $nano_admin_password
# Create a new VM on Hyper-V and load the just created Nano VHD
New-VM -Name $nano_servername  -VHDPath ".\$($nano_servername).vhd" -MemoryStartupBytes 1024MB
# Start the Nano VM
Start-VM -Name $nano_servername</pre>

&nbsp;

&nbsp;