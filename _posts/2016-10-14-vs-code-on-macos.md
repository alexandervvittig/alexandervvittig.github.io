---
id: 580
title: VS Code on macOS
date: 2016-10-14T15:09:52+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=580
permalink: /2016/10/14/vs-code-on-macos/
categories:
  - Uncategorized
---
I am starting to work more with VS Code, especially since it is so easy now to write PowerShell code on my MacBook Pro, without having to switch to a Windows VM or remote into a Windows machine.

Yet there a few kinks, they are however easy to fix.

  1. Install Powershell on the macOS
  
    So easy! Go to: [https://github.com/PowerShell/PowerShell/releases/
  
](https://github.com/PowerShell/PowerShell/releases/) Download the latest PowerShell package for macOS
  
    (It&#8217;s the one ending with .pkg)
  
    Allow the package to be run:
  
    System Preferences -> Security & Privacy -> Allow Apps downloaded from
  
    Follow the prompt
  
    Done.
  2. Installing the Powershell Extension
  
    Press &#8216;Shift+CMD+P&#8217; to open the Command Palett
  
    Type &#8216;Install Extensions&#8217;, select it and press enter
  
    Type in PowerShell, there is currently only a single extension from Microsoft for PowerShell, so that&#8217;s the one you should pick.
  
    Click on Install/Enable, restart VS Code, done.
  3. PowerShell Intellisense issues
  
    It seems to be common issue if there is no OpenSSL installed
  
    Have a read [here](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#1-powershell-intellisense-does-not-work-cant-debug-scripts) how to fix it.
  4. Another issue is PowerShell remoting. Since Windows is using win RM, macOS or Linux know nothing about that. You have to use SSH, specifically OpenSSH. You have to install that on your windows machine which is right now a little bit tricky ([step by step here](https://github.com/PowerShell/Win32-OpenSSH/wiki/Install-Win32-OpenSSH)) but eventually they are going to build a cmdlet or something to automate that for you.