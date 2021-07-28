---
layout: post
title: "Windows Terminal on Windows Server"
description: "Windows Terminal on Windows Server"
comments: true
keywords: "powershell"
---
Since most servers either don't have a Windows Store, or no access to a Windows Store, it was a bit silly from MSFT to release Windows Terminal ONLY to be installed via Windows Store.

If you DO have access to te Windows Store, you can just go to [https://aka.ms/terminal](https://aka.ms/terminal) and install it.

However if you want to Windows Terminal on a Server (and let's be honest, that's a much more likely use case?) you can do this:
1. Navigate to [https://github.com/microsoft/terminal/releases](https://github.com/microsoft/terminal/releases) and download the latest .msixbundle [do NOT click on it]
2. Rename the downloaded file to .zip
3. Extract the "CascadiaPackage_XXXX_x64.msix" and rename that .msix file to .zip
4. Extract the contents of that package
5. Run 'WindowsTerminal.exe'
6. Get come coffee :¬)

The downside of the method is you have to manually check and re-do this everytime there is a new version.

This is a dirty way of doing it automagically

``` PowerShell
$webData          = invoke-webrequest "https://github.com/microsoft/terminal/releases" -UseBasicParsing
$LatestBundle     = "https://github.com$(($web.links.href -match "msixbundle")[1])"
$downloadLocation = "C:\temp\WindowsTerminal"
$releaseName      = ($LatestBundle -split "/")[-1]
$fileDownload     = "$downloadLocation\$releaseName"

if(-not(test-path $downloadLocation)){new-item $downloadLocation -ItemType Directory -Force}
(New-Object Net.WebClient).DownloadFile($LatestBundle,$fileDownload)
$reName = Rename-Item $fileDownload -NewName ($fileDownload -replace "msixbundle","zip") -PassThru
Expand-Archive $reName.FullName -DestinationPath "$downloadLocation" 
Get-Childitem $downloadLocation | Where-Object {$_.name -notlike "*x64*"} | Remove-Item -Recurse -Force
$newName = Get-ChildItem $downloadLocation | foreach{ Rename-Item $_.fullname -NewName ($_ -replace "msix","zip") -PassThru}
Expand-Archive $newName.FullName -DestinationPath $downloadLocation
```
