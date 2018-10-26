---
id: 366
title: 'Minimal CentOS 7 &#8211; ifconfig depreciated'
date: 2015-12-13T11:17:39+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=366
permalink: /2015/12/13/minimal-centos-7-oh-my/
categories:
  - Linux
---
Being new to Linux, settings things up in CentOS it&#8217;s pain in the arse :o) Here some things I learned. If you have more than a few months Linux experiences, there might be nothing new for you here&#8230;

IFCONFIG does not work&#8230;

Apparently **ifconfig** has been depreciated. You can still install the package if needed:

<pre class="lang:default decode:true">yum -y install net-tools</pre>

It&#8217;s new replacement is **IP**

<pre class="lang:default decode:true ">ip a</pre>

If you want to learn more about it just use

<pre class="lang:default decode:true ">ip help
</pre>

Another way to setup IPs etc, I found handy are:

<pre class="lang:default decode:true  "># List installed ethernet cards
nmcli d 

# Open NetworkManager 
nmtui

# Set static IP
# e.g. "nmtui edit eth0"
nmtui edit &lt;connection&gt;

# Restart Network service after setting IP as needed
service network restart</pre>

&nbsp;

&nbsp;