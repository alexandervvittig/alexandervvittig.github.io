---
layout: post
title: "Force Jekyll rebuild on GitHub"
description: "Force Jekyll rebuild on GitHub"
comments: true
keywords: "PowerShell"
---
A cool little trick. Sometimes GitHub/Jekyll does not like to rebuild, just 'force' a rebuild by pushing an empty commit.

```PowerShell
git commit -m 'rebuild pages' --allow-empty
git push origin <branch-name>
```
