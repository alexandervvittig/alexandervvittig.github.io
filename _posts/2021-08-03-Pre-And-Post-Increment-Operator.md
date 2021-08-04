---
layout: post
title: "Pre and Post Increment Operator"
description: "Pre and Post Increment Operator"
comments: true
keywords: "PowerShell"
---
As myself, you might be super familiar with the increment/decrement operator
e.g.

``` PowerShell
++$i 
# vs
$i++
```
What was new to me, was that you can pre or post incrememnt, depending how you need it to behave!

Now, what's the difference?

``` PowerShell
$i = 0

do{
    $i
}
while(
    $i++ -le 5
)

# Output:
0123456
```

``` PowerShell
$i = 0

do{
    $i
}
while(
    ++$i -le 5
)

# Output:
012345
```

It basically dictates the behaviour of when the actual incementation is happening, BEFORE (pre-increment) the eval or AFTER (post-increment)

[Reference](https://devblogs.microsoft.com/scripting/pre-and-post-incrementing-do-while-loop-in-powershell/)
