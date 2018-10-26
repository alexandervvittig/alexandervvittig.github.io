---
id: 221
title: SQL Account locked out
date: 2015-07-16T11:50:48+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=221
permalink: /2015/07/16/sql-account-locked-out/
categories:
  - Break / Fix
  - SQL
---
While working on SQL (see my [previous post](http://blog.vvittig.com/2015/07/16/i-effing-hate-sql-and-vendor-support/)&#8230;) we of course got locked out&#8230;

I found a post that helped! (Thanks Google-fu!)

You can either run this query:

<pre class="lang:pgsql decode:true ">ALTER LOGIN sqluser WITH CHECK_POLICY = OFF;
ALTER LOGIN sqluser WITH CHECK_POLICY = ON;
GO</pre>

or via GUI, uncheck the box:

[<img class="aligncenter size-medium wp-image-222" src="http://blog.vvittig.com/wp-content/uploads/2015/07/sqluser-300x198.jpg" alt="sqluser" width="300" height="198" srcset="https://blog.vvittig.com/wp-content/uploads/2015/07/sqluser-300x198.jpg 300w, https://blog.vvittig.com/wp-content/uploads/2015/07/sqluser.jpg 332w" sizes="(max-width: 300px) 100vw, 300px" />](http://blog.vvittig.com/wp-content/uploads/2015/07/sqluser.jpg)

&nbsp;

PS: Dear Vendor, if you are selling a product, please know the ins and outs of the product AND the other products that are needed to get everything to work. Thank you.

Source:
  
<a href="http://www.sqldbadiaries.com/2010/07/21/unlock-sql-user-without-changing-the-password/#ixzz2OBIJCsqv" target="_blank">http://www.sqldbadiaries.com/2010/07/21/unlock-sql-user-without-changing-the-password/#ixzz2OBIJCsqv</a>

&nbsp;