---
id: 599
title: ConEmu the Windows\PowerShell console alternative
date: 2016-12-06T14:59:14+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=599
permalink: /2016/12/06/conemu-the-windowspowershell-console-alternative/
categories:
  - PowerShell
---
Ever wished you could have multiple consoles and stuff open without carefully rearranging them and then the Windows dock features messes it up and yaddi yadda?

Well, I found a superb solution for that: [ConEmu](https://conemu.github.io/)

[<img class="alignleft wp-image-600" src="http://blog.vvittig.com/wp-content/uploads/2016/12/ConEmu-Maximus5-300x205.png" alt="conemu-maximus5" width="500" height="341" srcset="https://blog.vvittig.com/wp-content/uploads/2016/12/ConEmu-Maximus5-300x205.png 300w, https://blog.vvittig.com/wp-content/uploads/2016/12/ConEmu-Maximus5.png 696w" sizes="(max-width: 500px) 100vw, 500px" />](http://blog.vvittig.com/wp-content/uploads/2016/12/ConEmu-Maximus5.png)

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

The 2 most handy commands you&#8217;ll need:

<pre class="lang:ps decode:true "># Split window horizontally:
powershell.exe -new_console:s

# Split window vertically:
powershell.exe -new_console:sV
</pre>

^ That is needed to create the Windows as you want. From there you can use them as regular console Windows. So handy!