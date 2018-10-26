---
id: 151
title: Hyper-V Server and Bitlocker without TPM
date: 2015-06-10T10:07:24+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=151
permalink: /2015/06/10/hyper-v-server-and-bitlocker-without-tpm/
categories:
  - Hyper-V
  - PowerShell
---
As I found out today, Hyper-V Server 2012 R2
  
<span style="color: #000000;">(the <a style="color: #000000;" href="https://www.microsoft.com/en-us/evalcenter/evaluate-hyper-v-server-2012-r2" target="_blank">FREE</a> version!)<strong> <span style="text-decoration: underline;">does support Bitlocker</span></strong>!</span> Hooray!

**Here is how to set it up:**

1. You have to install the Bitlocker feature.

<pre class="lang:ps decode:true"># Check all the Roles / Features
Get-WindowsFeature
# If Bitlocker is listed, install it
# I like to also add the Management tools
Install-WindowsFeature Bitlocker -IncludeAllManagementTools
# After install a reboot is needed
# You might as well include the  '-restart' parameter in the above command
shutdown -r -f -t 0</pre>

2. If you don’t have a TPM you will need to allow the use of Bitlocker without a TPM via GP. Either in your domain or via the local group policy snapin on the machine in question. To do that edit the following group policy key to “Enabled”.
  
Since we are on the Hyper-V Core machine, you have to [setup remote management first](http://blog.vvittig.com/2015/06/03/hyper-v-server-2016/), and make use of the **MMC -> Group Policy Object editor**.

<pre class="lang:default decode:true">Computer Configuration -&gt; Administrative Templates -&gt; Windows Components -&gt; Bitlocker Drive Encryption -&gt; Operating System Drives -&gt; Require additional authentication at startup</pre>

Make sure to check &#8220;**Alllow BitLocker without a compatible TPM**&#8221;

[<img class="aligncenter size-medium wp-image-155" src="http://blog.vvittig.com/wp-content/uploads/2015/06/BL-300x75.png" alt="BL" width="300" height="75" srcset="https://blog.vvittig.com/wp-content/uploads/2015/06/BL-300x75.png 300w, https://blog.vvittig.com/wp-content/uploads/2015/06/BL.png 316w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2015/06/BL.png)

3. Encrypting a drive with Bitlocker requires that a system administrator provides Bitlocker with one or more security protectors to protect the drive. I will be using a password, however one can also use a USB key and other methods to lock and unlock the Bitlocker volume.

<pre class="lang:ps decode:true"># manage-bde: invokes the script
# -protectors: defines what we are going to do (add protectors to the drive)
# -add: lets manage-bde know we are going to add a protectors to the drive
# C: defines which drive should receive the new protector
# -password: will allow us to set a self defined password to unlock the drive
# -recoverypassword generates a random recovery key 
manage-bde -protectors -add C: -password -recoverypassword</pre>

You should be prompted to enter you self defined password twice and you should receive a randomly generated recovery key printed on the screen. You should copy this down immediately so it’s not lost as it will be the only way to recover the volume if the user password is forgotten.

> HINT: To have the recovery key automatically saved to a USB thumb drive add the following to the end of the command:
> 
> <pre class="lang:ps decode:true ">-RecoveryKeyPath X:</pre>
> 
> Where X: should be the drive letter of the USB thumb drive.

Once the protectors have been put in place we can start the encryption of the volume with the following command:

<pre class="lang:ps decode:true "># -on: Lets manage-bde know we want to enable Bitlocker on the drive
# C: defines the drive which will be encrypted using Bitlocker
# In case you are encrypting a thin-provisioned virtual machine you will have to add the -usedspaceonly trigger at the end of the command to encrypt the volume
manage-bde -on C:</pre>

After the command is executed you will be prompted to restart your computer to complete the Bitlocker drive test. The test checks that you are able to log in to your system with Bitlocker enabled. Once the computer has restarted and you have made it back into Windows Bitlocker should start encrypting the drive.

You can keep an eye on the status of the encryption process with the following command:

<pre class="lang:ps decode:true ">manage-bde -status</pre>

Source:
  
<a href="http://jack-brennan.com/bitlocker-on-server-2012-and-hyper-v-server-core" target="_blank">http://jack-brennan.com/bitlocker-on-server-2012-and-hyper-v-server-core</a>