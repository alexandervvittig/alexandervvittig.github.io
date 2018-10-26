---
id: 282
title: PowerShell Clipboard History
date: 2015-10-07T20:00:45+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=282
permalink: /2015/10/07/powershell-clipboard-history/
categories:
  - PowerShell
---
I&#8217;m a big fan of <a href="https://smilesoftware.com/TextExpander/index.html" target="_blank">TextExpander</a> which is sadly MAC / OSX only. A pretty cool free alternative (but not yet quite as good, at least in the free version) is called <a href="http://www.phraseexpress.com/freeware.htm" target="_blank">PhraseExpress</a>. Making use of a clipboard history is really helpful, especially if you copy and paste a lot and don&#8217;t want to spend a lot of time, pressing UP UP UP UP UP just to eventually execute the wrong line.

PowerShell has it&#8217;s own version:

<pre class="lang:ps decode:true ">Get-History | Select-Object -ExpandProperty commandline | clip.exe</pre>

To copy only the last five commands, simply add the -Count parameter to Get-History:

<pre class="lang:ps decode:true">(Get-History -Count 5).CommandLine | clip.exe 
</pre>

Pretty cool huh? Now that is pretty long. Another way you can do this is like so:

<pre class="lang:ps decode:true ">Get-History | ogv</pre>

And you can get it even shorter by using the alias:

<pre class="lang:ps decode:true ">h | ogv</pre>

This is handy because you can search using the gridview search functionality and then copy one or more commands by simply highlighted the ones you want and hitting Ctrl-C.

If you are only doing this to find a command to re-execute, v3 and later this is handy:

<pre class="lang:ps decode:true ">h | ogv -p | r</pre>

&nbsp;