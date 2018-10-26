---
id: 346
title: SonicWall to AWS VPN
date: 2015-11-28T15:53:52+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=346
permalink: /2015/11/28/sonicwall-to-aws-vpn/
categories:
  - AWS
  - Networking
  - SonicWall
---
Today we are setting up a VPN between an onsite SonicWall and AWS.

  1. Log into your AWS account and navigate to your VPC
  2. [<img class="aligncenter size-full wp-image-347" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn01.png" alt="vpn01" width="237" height="160" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn01.png)Scroll down and navigate to **VPN Connections** -> **Customer Gateways**
  3. Click on **Create Customer Gateway**
  4. Name it, configure the routing and assign it the external IP address of your SonicWall (IP of the WAN interface)
  
    [<img class="aligncenter size-full wp-image-348" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn02.png" alt="vpn02" width="715" height="344" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn02.png 715w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn02-300x144.png 300w" sizes="(max-width: 715px) 100vw, 715px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn02.png)
  5. Navigate to **VPN Connections** -> **Virtual Private Gateways** and create a new Virtual Private Gateway and attach it to the VPC
  
    [<img class="aligncenter size-full wp-image-349" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn03.png" alt="vpn03" width="592" height="165" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn03.png 592w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn03-300x84.png 300w" sizes="(max-width: 592px) 100vw, 592px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn03.png)
  6. Navigate to **VPN Connections** -> **VPN Connections
  
** Create a new **VPN Connection**.
  
    [<img class="aligncenter size-full wp-image-350" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn04.png" alt="vpn04" width="736" height="385" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn04.png 736w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn04-300x157.png 300w" sizes="(max-width: 736px) 100vw, 736px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn04.png)
  7. Go to ‘Route Tables’ and add the private local route
  
    [<img class="aligncenter size-full wp-image-352" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn05.png" alt="vpn05" width="821" height="375" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn05.png 821w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn05-300x137.png 300w" sizes="(max-width: 821px) 100vw, 821px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn05.png)
  8. If all worked fine so far, go back to **VPN Connections** and download the Config File for the SonicWall. It has to the generic one as there is no specific one for SonicWall.
  
    [<img class="aligncenter size-full wp-image-353" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn06.png" alt="vpn06" width="699" height="345" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn06.png 699w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn06-300x148.png 300w" sizes="(max-width: 699px) 100vw, 699px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn06.png)
  9. You are done in AWS for now. **Take a coffee brake&#8230;** :o)
 10. Log into your SonicWall and navigate to:
  
    **VPN** -> **Settings** -> **VPN Policies** -> **Add&#8230;**
 11. <table>
      <tr>
        <td>
          Setup a VPN:<br /> IPSec Primary Gatey: AWS Tunnel 1 IP<br /> Shared Secret, see downloaded generic documentation (open in word!)<br /> Local IKE: Ext IP from Sonicwall<br /> Peer IKE: Same as IPSec Gateway
        </td>
      </tr>
    </table>
    
    [<img class="aligncenter size-full wp-image-355" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn07.png" alt="vpn07" width="638" height="408" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn07.png 638w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn07-300x192.png 300w" sizes="(max-width: 638px) 100vw, 638px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn07.png)</li> 
    
      * Setup the proposal accordingly:
  
        [<img class="aligncenter size-full wp-image-356" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn08.png" alt="vpn08" width="623" height="476" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn08.png 623w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn08-300x229.png 300w" sizes="(max-width: 623px) 100vw, 623px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn08.png)
      * Setup the Advances settings accordingly:
  
        [<img class="aligncenter size-full wp-image-357" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn09.png" alt="vpn09" width="644" height="413" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn09.png 644w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn09-300x192.png 300w" sizes="(max-width: 644px) 100vw, 644px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn09.png)
      * Go to **VPN** -> **Advanced** and disable **NAT Traversal**
  
        [<img class="aligncenter size-full wp-image-358" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn10.png" alt="vpn10" width="402" height="169" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn10.png 402w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn10-300x126.png 300w" sizes="(max-width: 402px) 100vw, 402px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn10.png)
      * Go to **Network** -> **Routing** and configure a new router for the VPN.
  
        [<img class="aligncenter size-full wp-image-359" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn11.png" alt="vpn11" width="386" height="417" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn11.png 386w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn11-278x300.png 278w" sizes="(max-width: 386px) 100vw, 386px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn11.png)
      * Go to **Firewall **-> **Access Rules** and create a new rule for the AWS VPN
  
        (**VPN** -> **LAN** and **LAN** -> **VPN)**
  
        [<img class="aligncenter size-full wp-image-360" src="http://blog.vvittig.com/wp-content/uploads/2015/11/vpn12.png" alt="vpn12" width="347" height="343" srcset="https://blog.vvittig.com/wp-content/uploads/2015/11/vpn12.png 347w, https://blog.vvittig.com/wp-content/uploads/2015/11/vpn12-300x297.png 300w" sizes="(max-width: 347px) 100vw, 347px" />](http://blog.vvittig.com/wp-content/uploads/2015/11/vpn12.png)
      * Check in both AWS and SonicWall that the tunnel is up and check the firewalls. Once that is done start pinging from local to AWS and vice versa to confirm all is good. 
        All done :o)</li> </ol>