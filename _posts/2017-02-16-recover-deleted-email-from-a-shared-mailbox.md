---
id: 621
title: Recover deleted email from a shared mailbox
date: 2017-02-16T18:01:21+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=621
permalink: /2017/02/16/recover-deleted-email-from-a-shared-mailbox/
categories:
  - PowerShell
---
We had a $user who deleted ALL emails from a shared mailbox and you might notice that the option to recover deleted items is grayed out and you cannot select it.

We need to set a registry key to turn that option on.

<pre class="lang:default decode:true ">Key for 32-bit Outlook on a 32-bit version of Windows
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Exchange\Client\Options
Key for 32-bit Outlook on a 64-bit version of Windows
HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Exchange\Client\Options
Key for 64-bit Outlook on a 64-bit version of Windows
HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Exchange\Client\Options</pre>

Create a new DWORD value with the name &#8216;DumpsterAlwaysOn&#8217; and a value of 1.

Easy via PowerShell:

<pre class="lang:ps decode:true ">if(!(test-path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Exchange\Client\Options")){
    New-Item -Path "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Exchange\Client" -Name 'Options'
    $props = @{
        # Pick the right path for your OS and Office Version
        path         = "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Exchange\Client\Options"
        name         = 'DumpsterAlwaysOn'
        value        = '1'
        propertytype = 'DWORD'
        force        = $true
        verbose      = $true
    }
    
    New-ItemProperty @props
}else{
    $props = @{
            # Pick the right path for your OS and Office Version
            path         = "HKLM:\SOFTWARE\Wow6432Node\Microsoft\Exchange\Client\Options"
            name         = 'DumpsterAlwaysOn'
            value        = '1'
            propertytype = 'DWORD'
            force        = $true
            verbose      = $true
        }
        
        New-ItemProperty @props
}</pre>

You have to close Outlook and start it again and voila, you can restore items.

[<img class="aligncenter size-full wp-image-623" src="http://blog.vvittig.com/wp-content/uploads/2017/02/restore.jpg" alt="" width="391" height="123" srcset="https://blog.vvittig.com/wp-content/uploads/2017/02/restore.jpg 391w, https://blog.vvittig.com/wp-content/uploads/2017/02/restore-300x94.jpg 300w" sizes="(max-width: 391px) 100vw, 391px" />](http://blog.vvittig.com/wp-content/uploads/2017/02/restore.jpg)

&nbsp;