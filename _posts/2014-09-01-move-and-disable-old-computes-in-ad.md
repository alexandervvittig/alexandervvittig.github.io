---
layout: post
title: "Move and Disable old computes in AD"
description: "Tutorial how to delete stuff in AD"
comments: true
keywords: "PowerShell"
---

---
layout: post
title: "What is Lorem Ipsum?"
description: "There is no one who loves pain itself, who seeks after it and wants to have it, simply because it is pain..."
comments: true
keywords: "dummy content, lorem ipsum"
---

Here’s a quick break down:

**dsquery computer –inactive 8 –limit 1000**
  
This line searches the AD for computers that have not logged in for 8 weeks or more. By default the dsquery will only look for 100 objects so we need to raise the limit.

**$comp -replace ‘”‘, ”**

Here we are cutting the “ character that dsquery hands the objects names over with. These are located at the start and end.

**Disable-ADObject** and **Move-ADObject** are self explanatory.
  
Note they do have –whatif switches that will help if you want to see whats going to happen.
  
Append -whatif to the end of the command.

<pre class="theme:sublime-text lang:ps decode:true ">$ADComputers = (dsquery computer -inactive 8 -limit 1000) -WhatIf
foreach ($comp in $ADComputers)
    {
        $compclean=($comp -replace ‘”‘, ”)
        Disable-ADAccount $compclean 
        Move-ADObject $compclean -Targetpath “ou=computers,ou=garbage,dc=domain,dc=com”      
    }</pre>

&nbsp;