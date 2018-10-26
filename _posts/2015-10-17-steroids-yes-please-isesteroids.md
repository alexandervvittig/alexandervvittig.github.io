---
id: 299
title: 'Steroids? &#8211; Yes please! ISESteroids'
date: 2015-10-17T18:15:44+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=299
permalink: /2015/10/17/steroids-yes-please-isesteroids/
categories:
  - PowerShell
  - Shout-Out
---
Just to rule things out of the bat, I am not talking about steroids for like sports, not I am talking about steroids for PowerShell. Huh? Yeah! Powershell!
  
<a href="http://www.powertheshell.com/isesteroids/" target="_blank">ISESteroids</a> is a PowerShell module, an add-on for the native PowerShell ISE. Sounds not too exciting but it is! Why?
  
Well, first of all, you do not need to install another application, not yet another editor, nope, it&#8217;s &#8216;just&#8217; an add-on.
  
Second, as it is &#8216;just&#8217; an add-on, you can run with minimal rights, thus no admin rights are needed to run it. Which is nice as my work computer, being it an enterprise and high security due to merchant processing, has only limited rights to what applications can be executed. As mentioned, no problem for the ISESteroids.

ISESteroids comes basically in 2 flavors, Professional and Enterprise.
  
(see for  a comparison <a href="http://www.powertheshell.com/isesteroids2/ordering-isesteroids/" target="_blank">here</a>)

Still not convinced? Let me show you a few examples how cool it is:

  1. As it is written as a module, a plug-in, it does not require administrative or other privileges to be used. As I work in a pretty secured environment I can not just install software on my laptop. It will be blocked and reported (yeah I actually tried&#8230;) so ISESteroids can still be used! Also, the install is super simple, download it, <span style="color: #ff9900;"><strong>unblock the zip</strong></span>, extract the zip, run the .bat file enjoy ISESteroids!
  
    <a href="http://www.powertheshell.com/isesteroids2/download/" target="_blank">Install details here</a>.
  2. It gives you &#8216;advise&#8217; and tips during regular coding (e.g. change not needed double quotes &#8221; to a single quote &#8216;) or it changes automatically from CLS to a PowerShell native command as in Clear-Host.
  
    [<img class="aligncenter wp-image-305 size-full" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell03.png" alt="powershell03" width="644" height="141" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell03.png 644w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell03-300x66.png 300w" sizes="(max-width: 644px) 100vw, 644px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell03.png) [<img class="aligncenter wp-image-306 size-full" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell01.png" alt="powershell01" width="517" height="113" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell01.png 517w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell01-300x66.png 300w" sizes="(max-width: 517px) 100vw, 517px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell01.png)Pretty handy huh!!?
  3. Another thing you will notice immediately once you installed ISESteroids, is that you suddenly have a ton of more buttons to click on.
  
    [<img class="aligncenter wp-image-304 size-full" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell02.png" alt="powershell02" width="797" height="249" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell02.png 797w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell02-300x94.png 300w" sizes="(max-width: 797px) 100vw, 797px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell02.png)
  4. Another feature that I love is applications. YES!! You can build .exe files straight from your PowerShell script. That used to be a major PITA to be able to get that to work. With ISE Steroids, a few click and voila, you have your own application. Awesome!
  
    [<img class="aligncenter size-full wp-image-309" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell04.png" alt="powershell04" width="691" height="205" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell04.png 691w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell04-300x89.png 300w" sizes="(max-width: 691px) 100vw, 691px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell04.png)
  5. It comes with a pretty powerful File version History / Revision change tracker
  
    [<img class="aligncenter size-full wp-image-313" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell05.png" alt="powershell05" width="992" height="296" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell05.png 992w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell05-300x90.png 300w" sizes="(max-width: 992px) 100vw, 992px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell05.png)
  6. Auto comment. How I hated it, you have to manually put a # in front of the line to comment it out. Starting in PowerShell Version 2 I think, they finally introduced the comment block <# Blah blah #> whitch which you could toggle whole sections to be commented out. ISESteroids has a nice little button for that build in.
  
    [<img class="aligncenter size-full wp-image-315" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell06.png" alt="powershell06" width="520" height="192" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell06.png 520w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell06-300x111.png 300w" sizes="(max-width: 520px) 100vw, 520px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell06.png)7. Did I already mentioned that I love snippet manager and text expander features, it just saves so much time. You can also read about that <a href="http://blog.vvittig.com/2015/10/07/powershell-clipboard-history/" target="_blank">here</a>.
  
    And you guessed it, ISESteroids comes with a build in Snippet Manager.
  
    [<img class="aligncenter size-full wp-image-316" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell07.png" alt="powershell07" width="581" height="369" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell07.png 581w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell07-300x191.png 300w" sizes="(max-width: 581px) 100vw, 581px" />](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell07.png)And my absolutely favorite part? You can define where the cursor is when you insert the snippet. I was missing that so much from TextExpander! Thank you Dr. Weltner!
  
    8.  Refactor &#8211; Clean up your scripts. Totally great feature. Love it, try it, use it!
  
    [<img class="aligncenter wp-image-318 size-medium" src="http://blog.vvittig.com/wp-content/uploads/2015/10/powershell08-232x300.png" alt="powershell08" width="232" height="300" srcset="https://blog.vvittig.com/wp-content/uploads/2015/10/powershell08-232x300.png 232w, https://blog.vvittig.com/wp-content/uploads/2015/10/powershell08.png 388w" sizes="(max-width: 232px) 100vw, 232px" />
  
](http://blog.vvittig.com/wp-content/uploads/2015/10/powershell08.png) There are many more features and options in this fantastic product, if you want to give it a shot, please go <a href="http://www.powertheshell.com/isesteroids2/" target="_blank">powertheshell.com/isesteroids2</a> and give it a test drive! :o)

&nbsp;

&nbsp;