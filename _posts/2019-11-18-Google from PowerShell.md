---
layout: post
title: "Google from PowerShell"
description: "Google from PowerShell"
comments: true
keywords: "powershell"
---
Ok, this is not new or rocketsurgery, but it's handy.

You can Google right out of the cmdline :¬)
Just add this to your PowerShell profile

```PowerShell
function google{
    if(-not($args.count -eq 0)){
        $searchstring = $args -join " " 
        $url = "https://www.google.com/search?q=$searchstring"
        $url = $url -replace "\s", "%20"
        Start-Process $Url
    }
}
```
