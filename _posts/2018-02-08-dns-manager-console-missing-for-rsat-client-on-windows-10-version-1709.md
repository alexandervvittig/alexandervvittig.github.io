---
id: 702
title: DNS manager console missing for RSAT client on Windows 10 Version 1709
date: 2018-02-08T15:46:58+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=702
permalink: /2018/02/08/dns-manager-console-missing-for-rsat-client-on-windows-10-version-1709/
categories:
  - Break / Fix
---
You might not even notice until you need it, but when you install the RSAT tools on Win 10 for 1709, the DNS manager console is missing. That&#8217;s exactly what happened to me. I needed to add some records in DNS and oops, where is it?

Well, there is a KB article on it, so there is a fix. :¬)

  1. Check if KB 2693643 is installed, if so uninstall it
  2. Create a temporary directory to put stuff in it
  3. Create a &#8220;installx64.bat&#8221; file with the following content: [assuming you run a 64 bit Windows] <pre class="lang:default decode:true">@echo off
md ex 
expand -f:* WindowsTH-RSAT_WS_1709-x64.msu ex\
cd ex
md ex
copy ..\unattend_x64.xml  ex\
expand -f:* WindowsTH-KB2693643-x64.cab ex\
cd ex
dism /online /apply-unattend="unattend_x64.xml"
cd ..\
dism /online /Add-Package /PackagePath:"WindowsTH-KB2693643-x64.cab"
cd ..\
rmdir ex /s /q</pre>
    
    4. Create a &#8220;unattend_x64.xml&#8221; file with the following content:
    
    <pre class="lang:default decode:true ">&lt;?xml version="1.0" encoding="UTF-8"?&gt;  
&lt;unattend xmlns="urn:schemas-microsoft-com:setup" description="Auto unattend" author="pkgmgr.exe"&gt;  
  &lt;servicing&gt;  
    &lt;package action="stage"&gt;  
      &lt;assemblyIdentity buildType="release" language="neutral" name="Microsoft-Windows-RemoteServerAdministrationTools-Client-Package-TopLevel" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" version="10.0.16299.2"/&gt;  
      &lt;source location="." permanence="temporary"/&gt;  
    &lt;/package&gt;  
  &lt;/servicing&gt;  
&lt;/unattend&gt;</pre>
    
    5. [Download the RSAT tools](https://www.microsoft.com/en-gb/download/details.aspx?id=45520) and put the msu file in the same folder
  
    [<img class="size-full wp-image-704 aligncenter" src="http://blog.vvittig.com/wp-content/uploads/2018/02/2018-02-08_15-45-30.png" alt="" width="243" height="83" />](http://blog.vvittig.com/wp-content/uploads/2018/02/2018-02-08_15-45-30.png)
    
    6. Start a command prompt with administrative permissions and run the &#8220;installx64.bat&#8221;
    
    Once completed, you should have your full set (including DNS) of RSAT tools back
    
    Resource: <https://support.microsoft.com/en-us/help/4055558></li> </ol>