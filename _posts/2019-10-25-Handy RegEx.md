---
layout: post
title: "Handy RegEx"
description: "Handy RegEx"
comments: true
keywords: "regex"
---

While I'm just a 'young padawan' in the great world of regex, I really enjoy its power and like using it. I mainly use it for quick fixes and string manipulation. Here are some handy snippets I use:

1. Have a long sausage of code seperated by semi-colon (;), try this:

```
Find: ;
Replace: $&\n
```

It will put each statement ending with ';' in a new line and you can actually read the scipt now

```
Before:
coffee;coffee;coffee;

After:
coffee;
coffee;
coffee;
```

2. Have a list and need to wrap it in quotes (" ")? Easy.

```
Find: (.+)
Replace: "$1" # or '$1' if you need single quotes
```

It'll basically wrap your strings with whatever you specify

```
Before:
coffee
coffee
coffee

After:
"coffee"
"coffee"
"coffee"
```

3. Now let's say you need those joint by comma in a line again

```
Find: \n
Replace: , # or whatever you need it to be separated with
```

It will join the lines back into one line separated by comma

```
Before:
"coffee"
"coffee"
"coffee"

After:
"coffee","coffee","coffee"
```

4. How about them pesky blank lines? I gatchu fam

```
Find: ^(?:[\t ]*(?:\r?\n|\r))+
Replace: <blank>
```

Now stick with me, that's where regex shows its true power and its crazy complexity
Let's look at the results.

```
Before:
"coffee"

"coffee"

"coffee"

After:
"coffee"
"coffee"
"coffee"
```

It does not look like much but if you have a larger script with hundrets of random blank lines in the code, it bothers me, this will fix it.

RegEx is stupid powerful, but with great power comes great resposibility. 

Yes it's complex and quite a beast to master but totally worth it and a great ROI
I barely scratched the surface of what all Regular Expressions can do, but I love using it for small quick fixes as I just posted about. They used to take quite a lot of time, cleaning lists and stuff up before you can use them. I now I can spend more time on the actual code, rather than cleaning 'dirty' input up!

https://docs.microsoft.com/en-us/dotnet/standard/base-types/regular-expression-language-quick-reference

