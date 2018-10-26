---
id: 179
title: Changing the Home Drive in AD
date: 2015-06-14T10:18:40+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=179
permalink: /2015/06/14/changing-the-home-drive-in-ad/
categories:
  - PowerShell
---
Since we are still moving things, we had to update the home drive location.

1. Get a list with all users who have a Home Drive set.

<pre class="lang:ps decode:true ">Get-ADUser -filter * -properties scriptpath, homedrive, homedirectory | ft Name, scriptpath, homedrive, homedirectory</pre>

2. I cleaned the list out and saved it as a .txt file

3. Then go through the list and update the Home Directory for each user in the list.

<pre class="lang:ps decode:true ">foreach ($SAM in Get-Content C:\HomeFolder.txt){
set-aduser $SAM -homedirectory \\&lt;UpdatedPath&gt;\$SAM -homedrive u:
}</pre>

&nbsp;