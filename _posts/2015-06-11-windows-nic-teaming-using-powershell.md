---
id: 172
title: Windows NIC Teaming using PowerShell
date: 2015-06-11T17:06:06+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=172
permalink: /2015/06/11/windows-nic-teaming-using-powershell/
categories:
  - PowerShell
---
A quick rundown how to NIC Team in Server Core:

1. We connect to the remote host and check what NICs are available to Team. We want to make a not of the adapter names.

<pre class="lang:ps decode:true"># Connect to the remote host
Enter-PSSession &lt;hostname&gt;
# List all the physicak adapters available to the machine
Get-NetAdapter -Physical</pre>

2. We create a new team and specify a name. Then we add NIC01 and NIC02 to the team.

<pre class="lang:ps decode:true"># Create a team called "TestTeam" and add NIC01 and NIC02 to the team
New-NetLbfoTeam -Name TestTeam -TeamMembers "NIC01", "NIC02"</pre>

3. Once we do that, the it will ask if it is ok and it will add the default settings:
  
_TeamingMode:&#8217;SwitchIndependent&#8217; and LoadBalancingAlgorithm:&#8217;Dynamic&#8217;</p> 

</em>**TeamingMode**

In this “**Switch Independent Mode**” the switches are not aware that different interfaces on the server comprise a team. Instead, all the teaming logic is done exclusively on the server.

There is also the option for “**Switch Dependent Mode**”, wherein all NICs that comprise the team are connected to the same switch for aggregation rather than redundancy.

**LoadBalancingAlgorithm</p> 

&#8212; Dynamic:
  
</strong>Uses the source and destination TCP ports and the IP addresses to create a hash for outbound traffic. Moves outbound streams from team member to team member as needed to balance team member utilization. When you specify this algorithm with the TeamingMode parameter and the SwitchIndependent value, inbound traffic is routed to a particular team member.**
  
&#8212; TransportPorts:
  
** Uses the source and destination TCP ports and the IP addresses to create a hash, and then assigns the packets that have the matching hash value to one of the available interfaces. When you specify this algorithm with the TeamingMode parameter and the SwitchIndependent value all inbound traffic arrives on the primary team member.**
  
&#8212; IPAddresses:
  
** Uses the source and destination IP addresses to create a hash, and then assigns the packets that have the matching hash value to one of the available interfaces. When you specify this algorithm with the TeamingMode parameter and the SwitchIndependent value, all inbound traffic arrives on the primary team member.**
  
&#8212; MacAddresses:
  
** Uses the source and destination MAC addresses to create a hash and then assigns the packets that have the matching hash value to one of the available interfaces. When you specify this algorithm with the TeamingMode parameter and the SwitchIndependent value, all inbound traffic arrives on the primary team member.**
  
&#8212; HyperVPort:
  
** Distributes network traffic based on the source virtual machine Hyper-V switch port identifier. When you specify this algorithm with the TeamingMode parameter and the SwitchIndependent value, inbound traffic is routed to the same team member as the switch port’s outgoing traffic.

4. Once that is done you should have a team

<pre class="lang:ps decode:true"># Check on the NIC Team status
Get-NetLLBfoTeam</pre>

We can check which NICs are the member, the status it is in, if it is up , or degraded
  
(mine was degraded since I only connected one NIC :oP)

Sources:
  
&#8211; <a href="https://technet.microsoft.com/en-us/library/jj130849(v=wps.630).aspx" target="_blank">https://technet.microsoft.com/en-us/library/jj130849(v=wps.630).aspx</a>
  
&#8211;<a href="http://www.windowsnetworking.com/articles-tutorials/windows-server-2012/windows-nic-teaming-using-powershell-part1.html" target="_blank">http://www.windowsnetworking.com/articles-tutorials/windows-server-2012/windows-nic-teaming-using-powershell-part1.html</a>