---
id: 128
title: Set mass ACL permissions
date: 2015-05-27T15:52:54+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=128
permalink: /2015/05/27/set-mass-acl-permissions/
categories:
  - Break / Fix
---
Alright so one of our customer&#8217;s shared drive broke, we were able to restore it and such, however the needed rights were gone. I found a cool nifty tool called &#8220;<a href="https://www.microsoft.com/en-us/download/details.aspx?id=23510" target="_blank">SubInACL</a>&#8221; to help me out. The default install is in

<pre class="lang:default decode:true ">C:\Program Files (x86)\Windows Resource Kits\Tools</pre>

The syntax for SubInCAL is like so:

<pre class="lang:default decode:true">SUBINACL /&lt;service&gt; \\MachineName\FOLDER\* /GRANT=[DomainName\]UserName[=Access]
</pre>

So in my case I used:

<pre class="lang:default decode:true">subinack /file D:\Data\* /grant=system=F
subinack /file D:\Data\* /grant=&lt;domainname&gt;\&lt;username&gt;=F
</pre>

The <access>parameter follows this list:

<p style="padding-left: 60px;">
  F : Full Control<br /> R : Generic Read<br /> W : Generic Write<br /> X : Generic eXecute<br /> L : Read controL<br /> Q : Query Service Configuration<br /> S : Query Service Status<br /> E : Enumerate Dependent Services<br /> C : Service Change Configuration<br /> T : Start Service<br /> O : Stop Service<br /> P : Pause/Continue Service<br /> I : Interrogate Service<br /> U : Service User-Defined Control Commands
</p>

To get all the sub-directories you can use the switch &#8216;_**/subdirectories**_&#8216;

Such an easy command saved the day!