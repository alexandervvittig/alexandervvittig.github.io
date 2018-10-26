---
id: 716
title: Wrap string with quotes
date: 2018-08-23T13:49:29+00:00
author: Alex W
layout: post
guid: https://blog.vvittig.com/?p=716
permalink: /2018/08/23/wrap-string-with-quotes/
categories:
  - PowerShell
  - RegEx
---
Have you ever found yourself needing to edit a long list with usernames, and you had to go in and manually clean that list up, format it properly, wrap it in quotes and so forth? Yeah, it&#8217;s painful, but I finally found this handy regex statement that makes it all better.

<pre class="lang:default decode:true">Expression:   (.+)
Replace with: '$1'</pre>

So let&#8217;s take we have a regular user list
  
[<img class="aligncenter size-full wp-image-722" src="https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-52-16.png" alt="" width="255" height="86" />](https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-52-16.png)

After running the regex, we have them all neatly wrapped in quotes

[<img class="aligncenter size-full wp-image-718" src="https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-23-16.png" alt="" width="609" height="139" srcset="https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-23-16.png 609w, https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-23-16-300x68.png 300w" sizes="(max-width: 609px) 100vw, 609px" />](https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-23-16.png)

Now we have this nice list, but let&#8217;s say we need that as a string in a line. regex? Yeah no problem!

<pre class="lang:default decode:true">Expression:   [\n\r]
Replace with: ,</pre>

[<img class="aligncenter size-full wp-image-720" src="https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-50-38.png" alt="" width="639" height="89" srcset="https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-50-38.png 639w, https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-50-38-300x42.png 300w" sizes="(max-width: 639px) 100vw, 639px" />](https://blog.vvittig.com/wp-content/uploads/2018/08/2018-08-23_13-50-38.png)

Oh so handy, hope it saves you some time!

EDIT:

Adding another, removing blank lines in a script

<pre class="lang:default decode:true ">^(?:[\t ]*(?:\r?\n|\r))+</pre>

Replace this with nothing to remove all empty lines. :¬)