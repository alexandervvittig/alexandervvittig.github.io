---
id: 612
title: 'Cluster shared folder &#8211; The object already exists'
date: 2016-12-30T12:04:04+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=612
permalink: /2016/12/30/cluster-shared-folder-the-object-already-exists/
categories:
  - Rambling
---
Grr run into this before, you create a new folder, give it a new name and somehow your cluster thinks, nah we already have that in there. I double and triple checked &#8216;Share and Storage Management&#8217;, there was no shared folder like that for sure.

Well, good &#8216;ol regedit to the rescue.

<pre class="lang:default decode:true ">HKLM\Cluster\Resources\&lt;GUID&gt;\Paramters\&lt;ShareName&gt;</pre>

And indeed, for some odd reason, there was a key with that name in there.

If you find a share that doesn&#8217;t belong, you can delete the key for the share on all nodes.

&nbsp;