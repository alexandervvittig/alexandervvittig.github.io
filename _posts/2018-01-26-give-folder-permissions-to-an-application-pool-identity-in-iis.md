---
id: 684
title: Give folder permissions to an Application Pool Identity in IIS
date: 2018-01-26T18:05:32+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=684
permalink: /2018/01/26/give-folder-permissions-to-an-application-pool-identity-in-iis/
categories:
  - Uncategorized
---
I keep forgetting this and have to look it up the few times I need it&#8230; so I&#8217;m going to post it here:

  1. When setting NTFS permissions, select local machine (not the domain or whatever)
  2. Add &#8220;IIS AppPool\DefaultAppPool&#8221;
  
    (Don&#8217;t forget to change &#8220;DefaultAppPool&#8221; here to whatever you named your application pool)

That&#8217;s it ¯\_(ツ)_/¯

&nbsp;