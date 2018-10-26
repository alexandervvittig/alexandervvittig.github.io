---
id: 491
title: My $profile
date: 2016-03-24T10:00:10+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=491
permalink: /2016/03/24/my-profile/
categories:
  - Uncategorized
---
In my previous post I talked about Powershell profiles, that is my current profile:

<pre class="lang:ps decode:true ">$br = "`r"
clear
if ($host.name -eq 'ConsoleHost')
{
$Shell=$Host.UI.RawUI
$size=$Shell.BufferSize
$size.width=120
$size.height=3000
$Shell.BufferSize=$size
$size=$Shell.WindowSize
$size.width=120
$size.height=30
$Shell.WindowSize=$size
$Shell.BackgroundColor="Black"
$Shell.ForegroundColor="White"
$Shell.CursorSize=10
$Shell.WindowTitle="Console PowerShell"
}
 
#PART 2
 
function Get-Uptime {
 
 $os = Get-WmiObject win32_operatingsystem
 $uptime = (Get-Date) - ($os.ConvertToDateTime($os.lastbootuptime))
 $Display = "" + $Uptime.Days + " days / " + $Uptime.Hours + " hours / " + $Uptime.Minutes + " minutes"
 Write-Output $Display
}
 
function Get-Time {return $(Get-Date | ForEach {$_.ToLongTimeString()})}
 
function prompt
{
 Write-Host "[" -noNewLine
 Write-Host $(Get-Time) -ForegroundColor Green -noNewLine
 Write-Host "] " -noNewLine
 Write-Host $($(Get-Location).Path.replace($home,"~")) -ForegroundColor cyan -noNewLine
 Write-Host $(if ($nestedpromptlevel -ge 1) { '&gt;&gt;' }) -noNewLine
 return "&gt; "
}
 
#PART 3
 
Set-Location C:\
 
$MaximumHistoryCount=1024
$IPAddress=@(Get-WmiObject Win32_NetworkAdapterConfiguration | Where-Object {$_.DefaultIpGateway})[0].IPAddress[0]
$IPGateway=@(Get-WmiObject Win32_NetworkAdapterConfiguration | Where-Object {$_.DefaultIpGateway})[0].DefaultIPGateway[0]
$PSExecPolicy=Get-ExecutionPolicy
$PSVersion=$PSVersionTable.PSVersion.Major
 
#PART 4
Write-Host "______________________________________________________________________________________________________________" -ForegroundColor Green
$br
Write-Host "|`tComputerName:`t`t" -nonewline -ForegroundColor Green;Write-Host $($env:COMPUTERNAME)"`t`t`t`t`t" -nonewline -ForegroundColor white;Write-Host "UserName:`t" -nonewline -ForegroundColor Green;Write-Host $env:UserDomain\$env:UserName"`t`t" -nonewline -ForegroundColor white
$br
Write-Host "|`tLogon Server:`t`t" -nonewline -ForegroundColor Green;Write-Host $($env:LOGONSERVER)"`t`t`t`t" -nonewline -ForegroundColor white;Write-Host "IP Address:`t" -nonewline -ForegroundColor Green;Write-Host $IPAddress"`t`t" -nonewline -ForegroundColor white
$br
Write-Host "|`tPS Execution Policy:`t" -nonewline -ForegroundColor Green;Write-Host $($PSExecPolicy)"`t`t`t" -nonewline -ForegroundColor white;Write-Host "`tPS Version:`t`t" -nonewline -ForegroundColor Green;Write-Host $PSVersion"`t`t`t" -nonewline -ForegroundColor white
Write-Host "|`tUptime:`t`t`t" -nonewline -ForegroundColor Green;Write-Host $(Get-Uptime)"`t`t`t`t`t`t" -nonewline -ForegroundColor white
$br
Write-Host "______________________________________________________________________________________________________________" -ForegroundColor Green
$br
</pre>

&nbsp;