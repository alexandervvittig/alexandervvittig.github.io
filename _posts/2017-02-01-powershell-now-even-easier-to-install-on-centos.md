---
id: 618
title: PowerShell now even easier to install on CentOS
date: 2017-02-01T15:20:02+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=618
permalink: /2017/02/01/powershell-now-even-easier-to-install-on-centos/
categories:
  - Linux
  - PowerShell
---
Want to use PowerShell on your CentOS box? Easier than ever!

<pre class="lang:default decode:true"># Change to root
sudo su 

# Register the Microsoft RedHat repository
curl https://packages.microsoft.com/config/rhel/7/prod.repo &gt; /etc/yum.repos.d/microsoft.repo

# Exit root mode
exit

# Install PowerShell
sudo yum install -y powershell

# Start PowerShell
powershell

# Update PowerShell
sudo yum update powershell</pre>

&nbsp;