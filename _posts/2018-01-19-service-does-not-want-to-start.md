---
id: 679
title: Service does not want to start
date: 2018-01-19T14:27:40+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=679
permalink: /2018/01/19/service-does-not-want-to-start/
categories:
  - Break / Fix
---
> The application has failed to start because the side-by-side configuration is incorrect

Ugh, yeah one of those&#8230; alright let&#8217;s have a look&#8230;

<pre class="lang:ps decode:true "># install your service
C:\Windows\Microsoft.NET\Framework[64]\[version]\InstallUtil.exe [path to application]

# uninstall your service
C:\Windows\Microsoft.NET\Framework[64]\[version]\InstallUtil.exe /u [path to application]

</pre>

So after (successfully) installing it, it does not want to start, so we have to do some tracing.

Eventlogs tells you only so much unfortunately so we look in the SxsTrace.exe  for help

<pre class="lang:default decode:true"># start trace
C:\windows\system32\SxsTrace.exe Trace -logfile:log.etl

# try to start your service
# press ENTER to stop the trace

# parse the trace logs
C:\windows\system32\SxsTrace.exe Parse -logfile:log.etl -outfile:SxSTrace.txt
</pre>

This will open the SxSTrace.txt file which will have all the information about the error.

If that did not create any helpful information (but I hope it did) there are other steps that might help:

<pre class="lang:default decode:true">Sfc /scannow
sfc /scannow /offbootdir=c:\ /offwindir=c:\windows (If above fails)</pre>

and let&#8217;s try DISM

<pre class="lang:default decode:true ">DISM.exe /Online /Cleanup-image /Scanhealth
DISM.exe /Online /Cleanup-image /Restorehealth</pre>

Last resort options are a System Restore or updating .NET to the latest version.

&nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;