---
id: 538
title: Install Bash on Windows 10
date: 2016-10-14T00:33:21+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=538
permalink: /2016/10/14/install-bash-on-windows-10/
categories:
  - Uncategorized
---
Yay bash! Still have not found a good powershell replacement for grep&#8230; sure there is &#8216;select-string&#8217; but meh&#8230;

Anyways how to install bash on Windows 10:

  1. Make sure you have the right version of Windows 10 and the Anniversary Update installed!
  2. Start -> Settings -> Update & Security -> For Developers -> Activate Developer Mode
  3. Go with Programs and Features (appwiz.cpl) and click on &#8216;Turn Windows features on or off&#8217;
  4. You should now see &#8220;**Windows Subsystem for Linux (Beta)**&#8220;
  5. Install it and run bash
  6. Now the most frustrating part, you have to sign in to the windows store and accept the TOS <pre class="lang:default decode:true"># Alternatively, this should work too!
lxrun /install /y</pre>

  7. Once finished you should have &#8220;Bash on Ubuntu on Windows&#8221;