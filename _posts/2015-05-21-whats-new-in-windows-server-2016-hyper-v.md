---
id: 101
title: 'What&#8217;s new in Windows Server 2016 Hyper-V'
date: 2015-05-21T18:32:18+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=101
permalink: /2015/05/21/whats-new-in-windows-server-2016-hyper-v/
categories:
  - Hyper-V
---
&nbsp;

[<img class="aligncenter size-full wp-image-103" src="http://blog.vvittig.com/wp-content/uploads/2015/05/Windows-Server-2016-Slider-Whats-new-in-Hyper-V.png" alt="Windows-Server-2016-Slider-Whats-new-in-Hyper-V" width="962" height="300" srcset="https://blog.vvittig.com/wp-content/uploads/2015/05/Windows-Server-2016-Slider-Whats-new-in-Hyper-V.png 962w, https://blog.vvittig.com/wp-content/uploads/2015/05/Windows-Server-2016-Slider-Whats-new-in-Hyper-V-300x94.png 300w, https://blog.vvittig.com/wp-content/uploads/2015/05/Windows-Server-2016-Slider-Whats-new-in-Hyper-V-960x299.png 960w" sizes="(max-width: 962px) 100vw, 962px" />](http://blog.vvittig.com/wp-content/uploads/2015/05/Windows-Server-2016-Slider-Whats-new-in-Hyper-V.png)

Look at all the awesome new features in Hyper-V server 2016. Really excited to give it a try!

Download your Technical Preview here:
  
<a href="https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-technical-preview?WT.mc_id=Blog_WS_Announce_TTD" target="_blank">https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-technical-preview?WT.mc_id=Blog_WS_Announce_TTD</a>

Just to name a few:

**Virtual Machine Protection**

  * Trust is the biggest blocker to cloud adoption
  * MS wants customers to know their data is secure
  * Virtual TPM and secure boot with Linux (Ubuntu 14.04 or later and SUSE)
  * Shielded Virtual Machines – Supports bitlocker inside of the VM, plus other features

**Isolation**

  * Storage QoS
  * Can set a policy that caps the IOPS across multiple VMs and they share the policy
  * Great for service providers
  * Host resource protection: Dynamically identify VMs that are not playing well and reduce their resource allocation. Can help protect against malware taking over resources.

**Availability**

  * Today, if you have a temp network outage the hyperV cluster will panic and fall apart in a very bad way. If the storage outage goes above 60 seconds, I/Os will fail and the guest OS will likely crash.
  * Virtual machine storage resiliency – VM is paused/suspended until storage access resumes
  * Virtual machine cluster resiliency – 4 minute timeout for cluster services being stopped, with automatic healing. Another resiliency feature for flapping cluster services due to HW issues, and the host will be quarantined and VMs live migrated off after a certain period.

**Shared VHDX**

  * Going to allow host based (agent free) backups with shared VHDXs
  * Now you can back up cluster as easy as standalone servers
  * Now allows online resizing of shared VHDXs
  * New VHDX type: VHDS

Replica support for hot add of VHDX. When you add a new disk it added it’s into the non-replicated set.

Runtime resize of memory – For Ws2016 and Windows 10, you can increase/decrease the runtime memory while the VM is running.

Hot add/remove of network adapters. Applicable to Generation 2 VMs only.

**Rolling cluster upgrade**

  * You can now upgrade a 2012 R2 Hyper-V to WS Tech Preview 2 with no downtime, no new hardware, and ability to rollback.

**Operational Improvements**

  * Production checkpoints – Uses VSS instead of saved state to create checkpoint. Fully supported in production. FINALLY!

**PowerShell Direct to Guest OS**

ReFS Accelerated VHDX Operations – Instant fixed disk creation and merging of checkpoints. “Instantly” create fixed disks in about 3 seconds of almost any size. Merging checkpoints happens without data being copied.

**Changing how we handle VM servicing**

  * Integration components are now distributed via Windows update

Evolving Hyper-V Backup: New architecture plus change block tracking is now native

VM Configuration files: VMCX and VMRS. Now a binary format efficient at scale

Source:
  
&#8211;<a href="http://blogs.technet.com/b/windowsserver/archive/2015/05/04/what-s-new-in-windows-server-2016-technical-preview-2.aspx" target="_blank">http://blogs.technet.com/b/windowsserver/archive/2015/05/04/what-s-new-in-windows-server-2016-technical-preview-2.aspx</a>