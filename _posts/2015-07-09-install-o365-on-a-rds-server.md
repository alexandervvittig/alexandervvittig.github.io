---
id: 211
title: Install O365 on a RDS Server
date: 2015-07-09T20:31:53+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=211
permalink: /2015/07/09/install-o365-on-a-rds-server/
categories:
  - Break / Fix
---
We have a Terminal Server and need to install Office without a Volume License.

According to <a href="http://technet.microsoft.com/en-us/library/jj900171.aspx" target="_blank">THIS</a>, that is allowed with E3 licensing.

[<img class=" wp-image-198 alignleft" src="http://blog.vvittig.com/wp-content/uploads/2015/07/o365-300x117.png" alt="o365" width="300" height="117" srcset="https://blog.vvittig.com/wp-content/uploads/2015/07/o365-300x117.png 300w, https://blog.vvittig.com/wp-content/uploads/2015/07/o365.png 1000w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2015/07/o365.png)

&nbsp;

&nbsp;

&nbsp;

So, a couple of things to note here:

1. RDS is <span style="text-decoration: underline;">not</span> permitted for Small Business premium
  
2. RDS <span style="text-decoration: underline;">IS</span> permitted for M, E3 and E4
  
3. There are no caveats or foot notes as there used to be

Now the actual question, HOW do you do it?

**Here the answer:**

1. Start by downloading the “<a href="http://www.microsoft.com/en-us/download/details.aspx?id=36778" target="_blank">Office Deployment Tool for Click-To-Run</a>” and extract it in a shared directory.

2. Navigate to your extracted folder (in our example \\server\o365) and edit the &#8216;configuration.xml&#8217; file following the <a href="https://technet.microsoft.com/en-us/library/jj219426.aspx" target="_blank">Microsoft guidelines</a>:

<pre class="lang:default decode:true ">&lt;Configuration&gt;
&lt;Add SourcePath="\\&lt;path&gt;\O365" OfficeClientEdition="32" &gt;
&lt;Product ID="O365ProPlusRetail"&gt;
&lt;Language ID="en-us" /&gt;
&lt;/Product&gt;
&lt;/Add&gt;
&lt;Updates Enabled="TRUE" /&gt;
&lt;Display Level="Full" AcceptEULA="TRUE" /&gt;
&lt;Property Name="SharedComputerLicensing" Value="1" /&gt;
&lt;/Configuration&gt;</pre>

3. Open CMD, navigate to the extraction folder (e.g. C:\O365) and run:

<pre class="lang:default decode:true ">setup.exe /download \\server\O365\configuration.xml</pre>

Let it run it will download the installer, it will create a new folder called &#8216;Office&#8217; and should be about 1GB once it finished.

4. Run the installer from CMD

<pre class="lang:default decode:true ">\\server\o365\setup.exe /configure \\server\o365\configure.xml</pre>

**Once that is done you should have O365 installed and it can be activated with individual O365 (E3) licenses. :o)**

&nbsp;

&nbsp;

&nbsp;