---
id: 117
title: 'Repoint a bunch of TSProfilePaths&#8230;'
date: 2015-05-25T12:14:16+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=117
permalink: /2015/05/25/repoint-a-bunch-of-tsprofilepaths/
categories:
  - PowerShell
---
We are still working on a migration for a LOT of users from a local infrastructure to solely working in the cloud. As part of that we have to move their roaming profiles in the cloud as well (why oh why did the previous MSP recommend roaming profiles&#8230; ;o( &#8230;). Anyways, so we moved the data via VPN and robocopy on the data server in AWS, however we still have to re-point the roaming profile path in AD. Sure enough there is no (or none that I found of anyways) way to easily re-point the _TSProfilePath_.

So I wrote a little script. I first got the SAMAccountName from all the users with a roaming profile and put them in a list.

Then went trough the list and updated the ADSI value for the _TerminalServicesProfilePath _value for each user in the list.

<pre class="lang:ps decode:true ">#  This AD is a mess so we don't need all the errors for non-existing (anymore) users 
$ErrorActionPreference= 'silentlycontinue'
# Get list.txt content for all roaming profile users
$List = Get-Content C:\list.txt
# Go through each line and get the line content (SAMAccountName)
foreach ($SAM in Get-Content C:\list.txt){

# Go to the SAMAccountName LDAP entry and update the TerminalServicesProfilePath
Get-ADUser $SAM | ForEach-Object  {
   $User = [ADSI]"LDAP://$($_.DistinguishedName)"
   $User.psbase.invokeset("TerminalServicesProfilePath","\\data\tsprofile\$SAM")
   $User.psbase.invokeset("TerminalServicesHomeDrive","H:")
   $User.psbase.invokeset("TerminalServicesHomeDirectory","") 
   $User.setinfo()
   }
}</pre>

&nbsp;