---
id: 588
title: Add a Group to Site Collection Administrators for Sharepoint Online
date: 2016-11-09T17:14:15+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=588
permalink: /2016/11/09/add-a-group-to-site-collection-administrators-for-sharepoint-online/
categories:
  - PowerShell
---
So since I just wasted more time than I want to admit getting this figured out, I&#8217; going to share here how to add  Group permissions. Googeling, there is not a whole lot of info about it out there and most sites even say it is not supported. There is unfortunately no &#8216;Get-SPOGroup&#8217; cmdlet, so PowerShell does not help in this case. Ugg, Microsoft, I thought that was the whole point of PowerShell!? Well, you can get the needed info via GUI.

The problem:

We need to be able to access and manage the SharePoint and mainly the OneDrive for Business content for users. We can do that easily via GUI, but going to the
  
**Sharepoint Admincenter -> User Profiles -> Type in a name -> Right-click on &#8216;Manage Site Collection Owners&#8217; -> Add the &#8216;AD Admin Group&#8217; **

[<img class="aligncenter size-medium wp-image-589" src="http://blog.vvittig.com/wp-content/uploads/2016/11/spol-300x193.png" alt="spol" width="300" height="193" srcset="https://blog.vvittig.com/wp-content/uploads/2016/11/spol-300x193.png 300w, https://blog.vvittig.com/wp-content/uploads/2016/11/spol.png 640w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2016/11/spol.png)

Now, that is all fine and dandy, but we have thousands of users, so if doing the above thousands of times, does not sound too fun. We also don&#8217;t have an intern handy to do this&#8230;

Now, the really frustrating part is, that you can not do that easily via PowerShell either!?!

<pre class="lang:ps decode:true ">Set-SPOUser -Site $sitename -LoginName $secondaryadmin -IsSiteCollectionAdmin $true -Verbose

# Error:
Set-SPOUser : The user does not exist or is not unique.</pre>

Now the good news is, yes you can do it via PowerShell, the bad news is, to get the needed info, you can not use PowerShell, you have to do some diggin&#8217; to get the SID form the Sharepoint Online GUI:

  1. Navigate to the root of the sharepoint site: <pre class="lang:default decode:true">https://yoursite.sharepoint.com/
</pre>

  2. Click on the gear/cog on the top right and click on  **&#8216;Site settings**&#8216;
  3. Under &#8216;Users and Permissions, click on &#8216;**Site permissions&#8217;**
  4. In the top ribbon, click on **&#8216;Check Permissions&#8217;**
  5. Type in the &#8216;AD ADMIN GROUP&#8217; name and click on &#8216;Check Now&#8217;

On the bottom you&#8217;ll see a tiny line coming up, giving you the SID of the group

<pre class="lang:default decode:true">Permission levels given to AD ADMIN GROUP (c:0-.f|rolemanager|s-1-5-21-123123123-123123123-123123123-123123123)</pre>

&nbsp;

The final PowerShell command to set the group permission for a single user is like so:

<pre class="lang:ps decode:true ">Set-SPOUser -Site 'https://yourdomain-my.sharepoint.com/personal/yourdomain' `
-LoginName 'c:0-.f|rolemanager|s-1-5-21-123123123-123123123-132123123-13123123' `
-IsSiteCollectionAdmin $true -Verbose</pre>

And the following script will iterate through all SPO users and assign the rights

<pre class="lang:ps decode:true "># Specify your organization admin central url 
$AdminURI 	  = 'https://yourdomain-admin.sharepoint.com'
# Specify the User account for an Office 365 global admin in your organization
$AdminAccount = 'adadmingroup@yourdomain'
$AdminPass    = 'yoursupersecurepasswordmuahahah'

# Specify the secondary admin account and the url for the onedrive site
# This is the SID that we had to get with a lof of clickedy GUI work
$secondaryadmin = 'c:0-.f|rolemanager|s-1-5-21-123123123-123123123-123123123-123123123'
$siteURI   = 'https://yourdomain-my.sharepoint.com' 

$loadInfo1 = [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SharePoint.Client')
$loadInfo2 = [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SharePoint.Client.Runtime')
$loadInfo3 = [System.Reflection.Assembly]::LoadWithPartialName('Microsoft.SharePoint.Client.UserProfiles')

$sstr           = ConvertTo-SecureString -string $AdminPass -AsPlainText -Force
$AdminPass      = ''
$creds          = New-Object Microsoft.SharePoint.Client.SharePointOnlineCredentials($AdminAccount, $sstr)
$UserCredential = New-Object System.Management.Automation.PSCredential -argumentlist $AdminAccount, $sstr

# Add the path of the User Profile Service to the SPO admin URL, then create a new webservice proxy to access it
$proxyaddr          = "$AdminURI/_vti_bin/UserProfileService.asmx?wsdl"
$UserProfileService = New-WebServiceProxy -Uri $proxyaddr -UseDefaultCredential False
$UserProfileService.Credentials = $creds

# Set variables for authentication cookies
$strAuthCookie = $creds.GetAuthenticationCookie($AdminURI)
$uri           = New-Object System.Uri($AdminURI)
$container     = New-Object System.Net.CookieContainer
$container.SetCookies($uri, $strAuthCookie)
$UserProfileService.CookieContainer = $container

# Sets the first User profile, at index -1
$UserProfileResult = $UserProfileService.GetUserProfileByIndex(-1)
Write-Host 'Starting- This could take a while.'
$NumProfiles       = $UserProfileService.GetUserProfileCount()
$i = 1

Connect-SPOService -Url $AdminURI -Credential $UserCredential

# As long as the next User profile is NOT the one we started with (at -1)...
While ($UserProfileResult.NextValue -ne -1) 
{
  Write-Host "Examining profile $i of $NumProfiles"
  # Look for the Personal Space object in the User Profile and retrieve it 
  # (PersonalSpace is the name of the path to a user's OneDrive for Business site. Users who have not yet created a  
  # OneDrive for Business site might not have this property set.)
  $Prop = $UserProfileResult.UserProfile | Where-Object { $_.Name -eq 'PersonalSpace' } 
  $Url  = $Prop.Values[0].Value

  # If OneDrive is activated for the user, then set the secondary admin
  if ($Url) {
    $sitename = $siteURI + $Url
    write-verbose $sitename -Verbose
    Set-SPOUser -Site $sitename -LoginName $secondaryadmin -IsSiteCollectionAdmin $true -ErrorAction SilentlyContinue -Verbose
    Write-Host "Added secondary admin to the site $($sitename)" 
  }

  # And now we check the next profile the same way...
  $UserProfileResult = $UserProfileService.GetUserProfileByIndex($UserProfileResult.NextValue)
  $i++
}
</pre>

Credit mainly goes to [http://www.jijitechnologies.com](http://www.jijitechnologies.com/blogs/add-remove-secondary-site-collection-admin-to-all-onedrive-for-business-users) for the iteration part.

I hope for you avid Googler who has to do the same, this will save you some time.

&nbsp;

&nbsp;