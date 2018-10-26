---
id: 690
title: Remote Variables
date: 2018-02-07T15:09:54+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=690
permalink: /2018/02/07/remote-variables/
categories:
  - PowerShell
---
I keep seeing many posts with people struggling to execute code on remote machines, it is usually not due to permissions issues, (enable PS Remoting), but mainly due to the fact that they forget that the remote machine does not know the value of the locally assigned variable.

### Using (new way) PSv3+

With PowerShell Version 3 and newer, $using was introduced.
  
If you want to pass a local variable to the remote machine , just add **$using:** in front of the variable name (e.g. **$using:localvariable**), and the local value will be given on to the remote machine. This is so much simpler and easier to read than the &#8216;old&#8217; argumentlist way.

<pre class="lang:ps decode:true "># Using '$using'
# PowerShell v3+
$localvalue01   = 'SampleValue01'
$localvalue02   = 'SampleValue01'

Invoke-Command -ComputerName $remotecomputer -ScriptBlock {
    write-output $using:localvalue01
    write-output $using:localvalue02
}</pre>

<h3 style="text-align: left;">
  Argumentlist (old way)
</h3>

In this sample, we are looking at using an argument list to pass the values of the variable to the remote machine.
  
You define the values you need per usual on your local machine, and then you add an **$argumentlist** as parameter.
  
The order you list the variables is important, as the one first variable listed is addressed with **$args[0]**, the variable next to it (to the right) is addressed with **$args[1]** and so forth.

<pre class="lang:ps decode:true "># Argument lists
# PowerShell v2 and lower
$localvalue01   = 'SampleValue01'
$localvalue02   = 'SampleValue02'

Invoke-Command -ComputerName $remotecomputer -ScriptBlock {
    write-output $args[0] #holds the value for $localvalue01
    write-output $args[1] #holds the value for $localvalue02
} -ArgumentList $localvalue01, $localvalue02</pre>

&nbsp;

Reference: [about\_remote\_variables](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/invoke-command?view=powershell-6)