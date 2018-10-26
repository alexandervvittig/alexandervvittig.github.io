---
id: 481
title: PowerShell Profiles
date: 2016-03-24T09:42:34+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=481
permalink: /2016/03/24/powershell-profiles/
categories:
  - PowerShell
---
If you work with Powershell, you most likely end up doing things multiple times and even eventually have the Console look the way YOU want and load modules and Ps-snapins as you need to. The best way to do that using Powershell profiles.

Profiles, especially starting out, can be a little bit confusing though, as there are actually 6 profiles.

[table id=3 /]

The most common one to use is most likely the &#8220;Current User, Current Host – ISE&#8221; or the &#8220;Current User, Current Host – console&#8221; profile.

The &#8216;$profile&#8217; variable points, depending if using the ISE or the console to the corresponding powershell script that has the profile information in it.

<pre class="lang:ps decode:true"># From Console
[1:52:36 PM] C:\&gt; $profile
C:\Users\awittig\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1</pre>

<pre class="lang:default decode:true "># From ISE
PS C:\&gt; $profile
C:\Users\awittig\Documents\WindowsPowerShell\Microsoft.PowerShellISE_profile.ps1</pre>

You can also get the hidden properties by using the **-Force** command:

<pre class="lang:ps decode:true ">[1:53:31 PM] C:\&gt; $PROFILE | fl * -Force


AllUsersAllHosts       : C:\Windows\System32\WindowsPowerShell\v1.0\profile.ps1
AllUsersCurrentHost    : C:\Windows\System32\WindowsPowerShell\v1.0\Microsoft.PowerShell_profile.ps1
CurrentUserAllHosts    : C:\Users\awittig\Documents\WindowsPowerShell\profile.ps1
CurrentUserCurrentHost : C:\Users\awittig\Documents\WindowsPowerShell\Microsoft.PowerShell_profile.ps1
Length                 : 75</pre>

To note, by default on a brand new computer there is no $profile there, so you have to create it on your own!

You can test if you have a powershell profile-file setup by running this command:

<pre class="lang:ps decode:true ">Test-Path $profile</pre>

The output should be a Boolean, either $true or $false. See below:

<a href="http://blog.vvittig.com/wp-content/uploads/2016/03/profile.png" rel="attachment wp-att-487"><img class="aligncenter size-full wp-image-487" src="http://blog.vvittig.com/wp-content/uploads/2016/03/profile.png" alt="profile" width="491" height="125" srcset="https://blog.vvittig.com/wp-content/uploads/2016/03/profile.png 491w, https://blog.vvittig.com/wp-content/uploads/2016/03/profile-300x76.png 300w" sizes="(max-width: 491px) 100vw, 491px" /></a>

As you can see, I do not have a profile file for the &#8216;CurrentUserAllHosts&#8217; parameter.

To create a new **$profile.CurrentUserAllHosts** profile we can do this:

<pre class="lang:ps decode:true ">new-item $PROFILE.CurrentUserAllHosts -ItemType file -Force</pre>

There are several ways to edit the file that you just created:

  1. You can just navigate to the **$profile.CurrentUserAllHosts** file and right click on it
  2. You can open it for editing in the ISE: <pre class="lang:ps decode:true">ise $profile.CurrentUserAllHosts
</pre>

  3. You can open it with notepad / explorer <pre class="lang:ps decode:true ">explorer $profile.CurrentUserAllHosts</pre>
    
    4. My favorite way, you can edit it with VIM
    
    <pre class="lang:default decode:true ">vim $profile.CurrentUserAllHosts</pre>
    
    (See my previous blog-post how to use vim for inline editing)</li> </ol> 
    
    &nbsp;