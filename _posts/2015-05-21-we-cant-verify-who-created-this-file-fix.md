---
id: 95
title: 'We can&#8217;t verify who created this file &#8211; FIX'
date: 2015-05-21T18:22:06+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=95
permalink: /2015/05/21/we-cant-verify-who-created-this-file-fix/
categories:
  - Break / Fix
---
We have  custom APP that is used internally only, and even though the UAC is disabled it was throwing this annoying error:

[<img class="aligncenter size-medium wp-image-96" src="http://blog.vvittig.com/wp-content/uploads/2015/05/security-warning.zoom60-300x199.jpg" alt="security warning.zoom60" width="300" height="199" srcset="https://blog.vvittig.com/wp-content/uploads/2015/05/security-warning.zoom60-300x199.jpg 300w, https://blog.vvittig.com/wp-content/uploads/2015/05/security-warning.zoom60.jpg 367w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2015/05/security-warning.zoom60.jpg)

The fix is relatively easy, you just have to be cautious as it might cause potential harm.

1. Navigate to: (<a href="https://technet.microsoft.com/en-us/sysinternals/bb963880.aspx" target="_blank">REGJUMP</a> is your best friend for that!)

<pre class="lang:default decode:true ">HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Policies\Associations</pre>

2. Add a new &#8216;String Value&#8217;, call it &#8216;LowRiskFileTypes&#8217; and give it the value &#8216;.exe&#8217;.
  
3. Make sure to remove the &#8216;.exe&#8217; from the &#8216;HighRiskFileTypes&#8217; list.
  
4. Reboot.

Again, the warning, <span style="color: #ff0000;"><strong>it poses extra risk</strong></span> as it **will not warn** when the user opens another &#8216;.exe&#8217; file. We have great backups, users only use the same apps and have no rights to install things, so I am comfortable applying it this way.