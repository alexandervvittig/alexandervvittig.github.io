---
id: 545
title: Upload pic to AD
date: 2016-08-17T15:46:22+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=545
permalink: /2016/08/17/upload-pic-to-ad/
categories:
  - PowerShell
---
Need to set pics in AD, here a quick way to do it with #powershell

<pre class="lang:ps decode:true ">$username  = Read-Host 'Please enter the sameaccountname'
$pathtopic = Read-Host 'Please provide the picture path'

# Set picture
$Picture   = [System.IO.File]::ReadAllBytes("$pathtopic")
Set-ADUser $username –add @{thumbnailphoto=$Picture}

# Download picture
$User      = Get-ADUser -identity $username –properties thumbnailphoto
$pathtopic = 'C:\Export.jpg'
[System.Io.File]::WriteAllBytes ($pathtopic, $User.Thumbnailphoto)

</pre>

If you are more comfortable with a GUI, [codetwo.com](http://www.codetwo.com/freeware/active-directory-photos/) has a free tool that will give you the same functionality.