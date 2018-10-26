---
id: 606
title: Lock your workstation via CMD or Powershell
date: 2016-12-21T20:49:09+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=606
permalink: /2016/12/21/lock-your-workstation-via-cmd-or-powershell/
categories:
  - PowerShell
---
First from CMD, that is pretty easy:

<pre class="lang:default decode:true ">rundll32.exe user32.dll, LockWorkStation</pre>

Now, with PowerShell, it is about the same, we call the user32.dll, just it is a little more work to get that to work right:

<pre class="lang:ps decode:true ">$script:nativeMethods = @();
function Register-NativeMethod([string]$dll, [string]$methodSignature)
{
    $script:nativeMethods += [PSCustomObject]@{ Dll = $dll; Signature = $methodSignature; }
}
function Add-NativeMethods()
{
    $nativeMethodsCode = $script:nativeMethods | foreach { "
        [DllImport(`"$($_.Dll)`")]
        public static extern $($_.Signature);
    " }
 
    Add-Type @"
        using System;
        using System.Runtime.InteropServices;
        public static class NativeMethods {
            $nativeMethodsCode
        }
"@
}
 
Register-NativeMethod "user32.dll" "bool LockWorkStation()"
Add-NativeMethods
[NativeMethods]::LockWorkStation()
</pre>

Credit for how to call DLLs from PowerShell goes to [Danny](https://blog.dantup.com/2013/10/easily-calling-windows-apis-from-powershell/).