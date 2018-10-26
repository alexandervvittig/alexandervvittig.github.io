---
id: 89
title: Copy NTFS permissions only and no data from source to target
date: 2015-05-18T18:03:44+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=89
permalink: /2015/05/18/copy-ntfs-permissions-only-and-no-data-from-source-to-target/
categories:
  - Break / Fix
---
We have a huge cloud migration coming up and have been syncing data for weeks now. It finally finished syncing, however the sync tool that we use broke the NTFS permissions&#8230; so I was looking for a way to export and import the NTFS permissions only.

<a href="https://technet.microsoft.com/en-us/library/cc753525.aspx" target="_blank">ICACLS</a> seem to work pretty good for that.

<pre class="lang:default decode:true ">Export --&gt; icacls "\\&lt;servername&gt;\Information\T-E-S-T" /save C:\ACL_info_file /T 
Import --&gt; icacls "\\&lt;servername&gt;\Information" /restore C:\ACL_info_file</pre>

Just a word of warning, the more files and folders you have, the longer it takes. The import took several hours for me.

Source:
  
&#8211; <https://marckean.wordpress.com/2013/01/03/copy-ntfs-permissions-only-and-no-data-from-source-to-target/>