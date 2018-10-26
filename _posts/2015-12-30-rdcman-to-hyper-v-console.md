---
id: 388
title: RDCMan to Hyper-V console
date: 2015-12-30T10:15:20+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=388
permalink: /2015/12/30/rdcman-to-hyper-v-console/
categories:
  - Hyper-V
---
I am a big fan of MSFT&#8217;s <a href="http://Remote Desktop Connection Manager" target="_blank">Remote Desktop Connection Manager</a>, I have dozens of servers in it at my work, so I started tinkering around with it at home, especially in mind connecting to all my VMs  on my Hyper-V test lab.

Turns out, is is not as straight forward as you&#8217;d think it&#8217;d be.

Here is how to get it to work:

  1. There are issues with the authentication. Adding the following registry keys fixes that: <pre class="lang:ps decode:true"># Run PowerShell as admin!
# Please remember, this is provided 'as-is'
# Think twice before executing code you are not sure what it does. :o) 
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowDefaultCredentials -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowDefaultCredentialsDomain -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowFreshCredentials -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowFreshCredentialsDomain -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowFreshCredentialsWhenNTLMOnly -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowFreshCredentialsWhenNTLMOnlyDomain -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowSavedCredentials -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowSavedCredentialsDomain -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
New-ItemProperty -Path HKLM:\SYSTEM\CurrentControlSet\Control\Lsa\Credssp\PolicyDefaults\AllowSavedCredentialsWhenNTLMOnly -Name Hyper-V -PropertyType String -Value "Microsoft Virtual Console Service/*" -Force
</pre>

  2. Even though you might be a local admin on the Hyper-V Host, add your account to the &#8216;Hyper-V Administrators&#8217; Group.
  3. Get the ID of the VM you want to connect to <pre class="lang:ps decode:true"># First use 'Get-VM' to get a list of all the VMs on your host
Get-VM
# Then get the ID
Get-VM "&lt;VMNAME&gt;" | select Id</pre>

  4. Now we can go to the RDCMan man and add a new server
  
    &#8211; Server name: _Is the name of your Hyper-V Host (NOT the VM)
  
_ &#8211; Check &#8216;VM console connect&#8217; and paste the ID we got via PowerShell
  
    &#8211; You can put whatever you want as &#8216;Display Name&#8217;
  
    <a href="http://blog.vvittig.com/wp-content/uploads/2015/12/2015-12-30_10-11-04.png" rel="attachment wp-att-390"><img class="aligncenter size-full wp-image-390" src="http://blog.vvittig.com/wp-content/uploads/2015/12/2015-12-30_10-11-04.png" alt="2015-12-30_10-11-04" width="367" height="130" srcset="https://blog.vvittig.com/wp-content/uploads/2015/12/2015-12-30_10-11-04.png 367w, https://blog.vvittig.com/wp-content/uploads/2015/12/2015-12-30_10-11-04-300x106.png 300w" sizes="(max-width: 367px) 100vw, 367px" /><br /> </a>
  5. Test and see if you can connect. To connect you have to provide the credentials to log in to the HYPER-V HOST, not the VM.

Now you should be able to use RdcMan to connect to your VMs, be it Window Linux, or anything else you can run as a VM. :o)