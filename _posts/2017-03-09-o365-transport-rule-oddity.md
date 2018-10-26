---
id: 627
title: O365 Transport Rule Oddity
date: 2017-03-09T10:47:34+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=627
permalink: /2017/03/09/o365-transport-rule-oddity/
categories:
  - PowerShell
---
Trying to block zip files with O365 seems a little painful, as the default GUI does not really give you the option (anymore?) If you Google, you might find screenshots with options to select the attachment but when I checked our GUI, that was all that I saw:

[<img class="aligncenter wp-image-628 size-medium" src="http://blog.vvittig.com/wp-content/uploads/2017/03/GUI-300x297.jpg" alt="" width="300" height="297" srcset="https://blog.vvittig.com/wp-content/uploads/2017/03/GUI-300x297.jpg 300w, https://blog.vvittig.com/wp-content/uploads/2017/03/GUI-150x150.jpg 150w, https://blog.vvittig.com/wp-content/uploads/2017/03/GUI.jpg 682w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2017/03/GUI.jpg)Clearly, there is no option to look for attachments, other than what the attachments CONTAIN.

So, trying PowerShell, something interesting happened.

<pre class="lang:ps decode:true ">New-TransportRule -Name 'Rule - Block password protected zip' -Priority '0' -Enabled $true `
-AttachmentExtensionMatchesWords 'zip' -RejectMessageReasonText 'Sorry your mail was blocked because it contained a zip file.' `
-StopRuleProcessing $true -SetAuditSeverity Low -SenderAddressLocation HeaderorEnvelope</pre>

Executing this PowerShell command, it created a new rule, that now had more/different options than the rule you could create from the GUI!

Look at this:[<img class="aligncenter wp-image-629 size-medium" src="http://blog.vvittig.com/wp-content/uploads/2017/03/attachment-262x300.jpg" alt="" width="262" height="300" srcset="https://blog.vvittig.com/wp-content/uploads/2017/03/attachment-262x300.jpg 262w, https://blog.vvittig.com/wp-content/uploads/2017/03/attachment.jpg 411w" sizes="(max-width: 262px) 100vw, 262px" />](http://blog.vvittig.com/wp-content/uploads/2017/03/attachment.jpg)

And now you can block file extensions and stuff to your heart&#8217;s content.

Oddities ¯\_(ツ)_/¯