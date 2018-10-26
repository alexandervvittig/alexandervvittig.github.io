---
id: 503
title: htop on CentOS 7
date: 2016-04-08T22:48:34+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=503
permalink: /2016/04/08/htop-on-centos-7/
categories:
  - Linux
---
Studying for the LFCS, I found a handy addition to **top**, called **<a href="https://en.wikipedia.org/wiki/Htop" target="_blank">htop</a>**.

The problem is the htop software package seems not to be part of the default **yum** repository. But the fix is easy, first install **epel **(Extra Packages for Enterprise Linux) and THEN you can install **htop**.

<pre class="lang:default decode:true "># 1. Install epel
yum -y install epel-release</pre>

<pre class="lang:default decode:true "># 2. Install htop
yum -y install htop</pre>

Done.