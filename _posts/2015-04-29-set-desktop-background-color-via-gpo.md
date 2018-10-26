---
id: 42
title: Set desktop background color via GPO
date: 2015-04-29T00:35:47+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=42
permalink: /2015/04/29/set-desktop-background-color-via-gpo/
categories:
  - GPO
---
There is no default GPO to set the Desktop background. We have a terminal server with a white wallpaper, however the default background is black, thus you can not read the icon&#8217;s font. To fix that, you can create an ADM template.

<pre class="lang:coffee decode:true ">CLASS USER
CATEGORY !!categoryname
KEYNAME "Control Panel\Colors"
POLICY !!policyname
EXPLAIN !!explaintext
PART !!labeltext DROPDOWNLIST REQUIRED
VALUENAME "Background"
ITEMLIST
NAME "Black" VALUE "0 0 0"
END ITEMLIST
END PART
END POLICY
END CATEGORY
[strings]
categoryname="Background Color Options"
policyname="Change the background color of the client computer"
explaintext="This policy sets the background color of the client computer"
labeltext="Choose a color"</pre>

Save that file to your server and name it &#8216;backgroundcolor.adm&#8217;. Open up Group Policy Management and create a new  GPO and link it to the right OU.
  
Edit the GPO, go to User Configuration -> Administrative Templates, right click Administrative Templates and then Add Template

Browse to the Backgroundcolor.adm and add it in. Under Administrative Templates you will now see a custom category called “Set Background Color”

To change the colour of the desktop, select “Desktop Background Color policy”, then enable it.

Simply then enter the RGB value of the color you want.