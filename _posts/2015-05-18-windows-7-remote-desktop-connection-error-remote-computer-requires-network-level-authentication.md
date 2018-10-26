---
id: 84
title: 'Windows 7 Remote Desktop Connection error: Remote computer requires Network Level Authentication'
date: 2015-05-18T13:05:59+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=84
permalink: /2015/05/18/windows-7-remote-desktop-connection-error-remote-computer-requires-network-level-authentication/
categories:
  - Break / Fix
---
I run today into an odd issue, a user was not able to to RDP into their new Terminal Server.

[<img class="aligncenter wp-image-85 size-full" src="http://blog.vvittig.com/wp-content/uploads/2015/05/RDC1.jpg" alt="RDC1" width="400" height="157" srcset="https://blog.vvittig.com/wp-content/uploads/2015/05/RDC1.jpg 400w, https://blog.vvittig.com/wp-content/uploads/2015/05/RDC1-300x118.jpg 300w" sizes="(max-width: 400px) 100vw, 400px" />](http://blog.vvittig.com/wp-content/uploads/2015/05/RDC1.jpg)

&nbsp;

When you check on the RDP connection tab it says NLA is <span style="text-decoration: underline;"><strong>not</strong></span> supported.

[<img class="aligncenter size-medium wp-image-86" src="http://blog.vvittig.com/wp-content/uploads/2015/05/RDC2-300x188.jpg" alt="RDC2" width="300" height="188" srcset="https://blog.vvittig.com/wp-content/uploads/2015/05/RDC2-300x188.jpg 300w, https://blog.vvittig.com/wp-content/uploads/2015/05/RDC2.jpg 400w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2015/05/RDC2.jpg)

The cause seems to be an issue with a DLL file in the Registry.

And here is fix:

**Configure Network Level Authentication**
  
1. Click Start, click Run, type regedit, and then press ENTER.
  
2. In the navigation pane, locate and then click the following registry subkey: HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa
  
3. In the details pane, right-click Security Packages, and then click Modify.
  
4. In the Value data box, type tspkg. Leave any data that is specific to other SSPs, and then click OK.
  
5. In the navigation pane, locate and then click the following registry subkey: HKEY\_LOCAL\_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders
  
6. In the details pane, right-click SecurityProviders, and then click Modify.
  
7. In the Value data box, type credssp.dll. Leave any data that is specific to other SSPs, and then click OK.
  
8. Exit Registry Editor.
  
9. Restart the computer.

&nbsp;

Sources:
  
&#8211; <http://www.powercram.com/2009/07/enabling-network-level-authentication.html#>
  
&#8211; <https://community.dynamics.com/gp/b/gpdynland/archive/2013/07/26/windows-7-remote-desktop-connection-error-remote-computer-requires-network-level-authentication>