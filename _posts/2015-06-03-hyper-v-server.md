---
id: 142
title: How to manage Hyper-V Server
date: 2015-06-03T16:39:40+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=142
permalink: /2015/06/03/hyper-v-server/
categories:
  - Break / Fix
  - Hyper-V
---
Since managing it remotely in anon domain environment is a pain in the neck and I&#8217;ll have to setup quite a few servers in the next couple of weeks, here a quick &#8216;how to&#8217; mange Hyper-V Server 2016 remotely.

**SERVER CONFIGURATION**

1. Run

<pre class="lang:default decode:true ">sconfig</pre>

2. Configure Remote Management + ping (Opt. 4 -> Opt. 4 -> Opt. 1)
  
3. Enabled Remote Desktop (Opt. 7 -> e -> Opt. 2)
  
4. Run this command to allow RDP through the server&#8217;s firewall:

<pre class="lang:ps decode:true ">netsh advfirewall firewall set rule group="remote desktop" new enable=Yes</pre>

5. Launch Powershell and execute this command:

<pre class="lang:ps decode:true ">Install-WindowsFeature –Name Hyper-V –IncludeManagementTools –Restart</pre>

**
  
CLIENT CONFIGURATION
  
** 

1. Add an entry to the hostfile as you can not add a Hyper-V server via IP
  
(e.g. 192.168.1.1 HOSTSRV01.WORGROUP HOSTSRV01)

2. Run -> **dcomcnfg**, right-click on &#8216;My Computer&#8217; -> Properties -> COM Security Tab -> Access Permissions -> Edit Limits -> Anonymous Logon -> Allow &#8216;Local & Remote&#8217; Access

3.

<pre class="lang:default decode:true ">cmdkey /add:&lt;HostServerName&gt; /user:&lt;AdminUsername&gt; /pass:"&lt;Password&gt;"</pre>

4. Install the RSAT Tools for your Operating system. Open the Server Manager and add the Hyper-V host as a server.

5. You should get a permission error, run the following command:

<pre class="lang:ps decode:true ">Set-Item wsman:\localhost\Client\TrustedHosts &lt;HostServerName&gt; -Concatenate -Force</pre>

Now you should be able to remote manage / create / edit your Hyper-V Server.

&nbsp;