---
id: 477
title: VIM and Powershell
date: 2016-03-22T12:31:34+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=477
permalink: /2016/03/22/vim-and-powershell/
categories:
  - PowerShell
---
I love Powershell, but a feature that seems &#8216;missing&#8217; or not so well developed seems to be inline editing. Like, you know in Linux, you use nano or emacs or [vim](https://www.linux.com/learn/tutorials/228600-vim-101-a-beginners-guide-to-vim). Luckily, there is [vim for Windows](http://www.vim.org/download.php)!

All you need to do is download the executable and move it in you &#8216;Windows/System32&#8217; folder and you can use it like you are used ti from Linux.

So let&#8217;s say you want to to edit your Powershellprofile?

<pre class="lang:ps decode:true ">vim $profile</pre>

let&#8217;s you edit it in the Powershell console.

Really been missing an inline editor!

Sure you can just do this:

<pre class="lang:default decode:true ">explorer $profile
</pre>

However editing files inline with the power of vim, it&#8217;s fantastic!

<a href="http://blog.vvittig.com/wp-content/uploads/2016/03/vim.png" rel="attachment wp-att-478"><img class="aligncenter size-full wp-image-478" src="http://blog.vvittig.com/wp-content/uploads/2016/03/vim.png" alt="vim" width="686" height="427" srcset="https://blog.vvittig.com/wp-content/uploads/2016/03/vim.png 686w, https://blog.vvittig.com/wp-content/uploads/2016/03/vim-300x187.png 300w" sizes="(max-width: 686px) 100vw, 686px" /></a>

&nbsp;

&nbsp;

&nbsp;