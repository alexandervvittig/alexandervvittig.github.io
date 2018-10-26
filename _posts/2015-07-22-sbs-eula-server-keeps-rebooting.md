---
id: 238
title: 'SBS EULA &#8211; Server keeps rebooting'
date: 2015-07-22T12:58:12+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=238
permalink: /2015/07/22/sbs-eula-server-keeps-rebooting/
categories:
  - Break / Fix
---
We had a SBS server that is no longer in use but still has important information on it. The second you have an other DC on the Domain SBS starts to freak out a little as it violates the EULA (so does turning the SBS Core service off&#8230;) The problem is as long as the SBS server sees there is another DC, it will keep turning off every hour. VERY frustrating.

The below is the error log you should see:
  
[<img class="aligncenter size-medium wp-image-239" src="http://blog.vvittig.com/wp-content/uploads/2015/07/sbcore_tmb-270x300.png" alt="sbcore_tmb" width="270" height="300" srcset="https://blog.vvittig.com/wp-content/uploads/2015/07/sbcore_tmb-270x300.png 270w, https://blog.vvittig.com/wp-content/uploads/2015/07/sbcore_tmb.png 282w" sizes="(max-width: 270px) 100vw, 270px" />](http://blog.vvittig.com/wp-content/uploads/2015/07/sbcore_tmb.png)

To disable we followed the below:

  1. Download the Process Explorer tool from SysInternals – <a href="http://technet.microsoft.com/en-us/sysinternals/bb896653.aspx" target="_blank">Here</a>
  2. Load Process Explorer and look for the SBS Licensing Service – C:\Windows\system32\sbscrexe.exe
  3. Select this service and Suspend it – you should find the service greys out
  4. Open Regedit and expand the following key – HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Services\SBCore
  5. Right click this Key and add the Administrators group giving them Full Permission to the key (refresh this and you should see all the key entries now)
  6. Select the Start DWORD and change it from 2 to 4 (this sets the Disabled state)
  7. Open a File Explorer window and browse to the C:\Windows\system32\sbscrexe.exe file
  8. Right click this and load Properties / Security
  9. Add the Everyone group and set the Deny permission for Full Access (should then tick the sub permissions)
 10. Go back to Process Explorer and now kill the sbscrexe.exe service – this should now be disabled
 11. Check the SBCore service via services.msc – it should have a disabled state and now longer be running
 12. Get some coffee &#8211; you saved the day. ;o)

Source:
  
<a href="http://www.webbosworld.co.uk/blog/?p=175" target="_blank">http://www.webbosworld.co.uk/blog/?p=175</a>