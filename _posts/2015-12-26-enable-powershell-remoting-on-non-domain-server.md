---
id: 376
title: Enable PowerShell Remoting on non-domain server
date: 2015-12-26T13:52:47+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=376
permalink: /2015/12/26/enable-powershell-remoting-on-non-domain-server/
categories:
  - PowerShell
---
Here a quick &#8216;how to&#8217; connect to a remote server via PowerShell that is not joined to a domain.

**
  
On remote server:
  
** 1. Make sure the Windows Remote Management (winrm) service is running

<pre class="lang:ps decode:true "># Get the status of the winrm service
Get-Service winrm
# If it not running, start the service
Start-Service winrm
# Also set the service to start automatically (Delayed Start)
Set-Service "winrm" -StartupType Automatic
# Enable winrm 
winrm quickconfig</pre>

2. Make sure your network connection type is private

<pre class="lang:ps decode:true "># To see if it's set to private or not run this
Get-NetConnectionProfile
# To set it to Private, run this (as admin)
Set-NetConnectionProfile -NetworkCategory Private</pre>

3. Enable PowerShell remoting

<pre class="lang:ps decode:true ">Enable-PSRemoting -Force</pre>

**
  
On local computer:
  
** 

1. Make sure the Windows Remote Management (winrm) service is running

<pre class="lang:ps decode:true"># Get the status of the winrm service
Get-Service winrm
# If it not running, start the service
Start-Service winrm
# Also set the service to start automatically (Delayed Start)
Set-Service "winrm" -StartupType Automatic</pre>

2. Add the &#8216;remote server&#8217; to the trusted host list

<pre class="lang:ps decode:true"># Add your 'remote server's' IP to the trusted host list
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "192.168.1.1" -Force
# Or if IPs are constantly changing, add ALL IPs (* is the wildcard)
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "*" -Force
# Check and make sure the right value is in the trusted host list
Get-Item WSMan:\localhost\Client\TrustedHosts
# To clear the trusted host list, run this
Set-Item WSMan:\localhost\Client\TrustedHosts -Value "" -Force</pre>

&nbsp;

**Connect to your remote server:**

<pre class="lang:default decode:true "># If you are in CLI
Enter-PSSession -ComputerName 192.168.1.1 -Credential Get-Credential
# If you are in the ISE
$credential = Get-Credential
Enter-PSSession -ComputerName 192.168.1.1 -Credential $credential</pre>

If everything went right, you should see a prompt showing the remote PC IP

<pre class="lang:ps decode:true"># e.g. like this:
[192.168.1.1]: PS C:\Users\Administrator&gt;</pre>

&nbsp;

&nbsp;

&nbsp;