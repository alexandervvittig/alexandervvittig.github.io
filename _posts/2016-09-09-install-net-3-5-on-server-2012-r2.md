---
id: 552
title: Install .NET 3.5 on Server 2012 R2
date: 2016-09-09T13:57:15+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=552
permalink: /2016/09/09/install-net-3-5-on-server-2012-r2/
categories:
  - Uncategorized
---
As this is a very common &#8216;issue&#8217; I am just going to post the quick-fix:

If you have internet:

<pre class="lang:ps decode:true">DISM /online /enable-feature /featurename:netfx3 /all</pre>

Install from install media:

<pre class="lang:ps decode:true "># Where 'd' is the drive the install media is mounted to. You might have
# to change it if your media is on a different drive letter
DISM /Online /Enable-Feature /FeatureName:NetFx3 /All /LimitAccess /Source:d:\sources\sxs</pre>

&nbsp;