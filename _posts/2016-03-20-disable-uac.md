---
id: 466
title: Disable UAC with Powershell
date: 2016-03-20T11:27:07+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=466
permalink: /2016/03/20/disable-uac/
categories:
  - PowerShell
---
The User Account Control (UAC) is an important security feature of Windows. Yet setting up a server, clicking a gazillion times on the silly UAC prompt, is VERY frustrating.

Let&#8217;s turn it off until we are done, and then turn it back on.

<pre class="lang:ps decode:true  ">Clear-Host
$reg = Get-ItemProperty HKLM:Software\Microsoft\Windows\CurrentVersion\policies\system\
$UAC = $reg.EnableLUA

switch ($UAC){
1   {
            $disableuac = Read-Host "UAC is enabled, do you want to disable it? [Y/N]"
            if($disableuac -eq 'Y' -or $disableuac -eq 'y'){
            New-ItemProperty -Path HKLM:Software\Microsoft\Windows\CurrentVersion\policies\system -Name EnableLUA -PropertyType DWord -Value 0 -Force
            $reboot = Read-Host "For this change to take effect you have to reboot. Reboot now? [Y/N]"
            if($reboot -eq 'Y' -or $reboot -eq 'y'){
            restart-computer -Force
            }else{
            Write-Output "Reboot later."
            }}
        }
0       {$enableuac = Read-Host "UAC is disabled, do you want to enable it? [Y/N]"
            if($enbleuac -eq 'Y' -or $enableuac -eq 'y'){
            New-ItemProperty -Path HKLM:Software\Microsoft\Windows\CurrentVersion\policies\system -Name EnableLUA -PropertyType DWord -Value 1 -Force
            $reboot = Read-Host "For this change to take effect you have to reboot. Reboot now? [Y/N]"
            if($reboot -eq 'Y' -or $reboot -eq 'y'){
            restart-computer -Force
            }else{
            Write-Output "Reboot later."
            }}
        }
default {Write-Output "Oops, something went wrong"}
}
</pre>

&nbsp;

[table id=2 /]