---
id: 645
title: Allow mail enabled Public Folders in o365 to accept mail from external domains
date: 2017-06-29T13:49:18+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=645
permalink: /2017/06/29/allow-mail-enabled-public-folders-in-o365-to-accept-mail-from-external-domains/
categories:
  - Active Directory
  - o365
  - PowerShell
---
So you are in a hybrid environment and moved your Public Folders to o365 but suddenly 3rd party people can no longer send you emails?

Yeah&#8230; try this:

<pre class="lang:ps decode:true "># For all Public Folders
Get-PublicFolder -Recurse | 
Add-PublicFolderClientPermission -User Anonymous -AccessRights CreateItems

# For a specific Public Folder
Get-PublicFolder -identity "\Folder" | 
Add-PublicFolderClientPermission -User Anonymous -AccessRights CreateItems</pre>

&nbsp;