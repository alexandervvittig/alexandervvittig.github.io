---
layout: post
title: "Unable to resolve package source"
description: "Unable to resolve package source"
comments: true
keywords: "powershell"
---
If you are running an older version of TLS and try to interact with the PowerShell Gallery you may see error messages like:
> WARNING: Unable to resolve package source 'https://www.powershellgallery.com/api/v2'

The [gallery](https://www.powershellgallery.com/) officially only supports TLS 1.2, so you have to use this as a workaround:

```PowerShell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
```

[READ MORE HERE](https://devblogs.microsoft.com/powershell/powershell-gallery-tls-support/)
