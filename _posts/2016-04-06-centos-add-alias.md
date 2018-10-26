---
id: 500
title: CentOS Add alias
date: 2016-04-06T18:00:42+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=500
permalink: /2016/04/06/centos-add-alias/
categories:
  - Linux
---
Now that I scheduled my LFCS exam I am trying to spend more time with Linux. A big pet peeve of mine is that CLS and CLEAR are not the same thing, one works in CMD one works in the CLI but you can&#8217;t interchange them between Linux and Windows.

( Yet PowerShell is happy with either&#8230;!)

So to make life easier here how to add an alias in CentOS so both clear and CLS will work:

Aliases are defined in the .bashrc file on root. Can&#8217;t see it? It&#8217;s a hidden file so &#8216;ls -al&#8217; should do the trick. See it now?

We can edit it just with vi:

vi .bashrc

The line we want to append should look like so:

alias keyword=&#8217;target&#8217;

So in my case: alias cls=&#8217;clear&#8217;

Keyword is the word you&#8217;d enter and target is the word / command that will actually be entered in the shell/CLI.

You&#8217;ll need to restart the shell or log out and back in again for it to work. Also make sure to save your .bashrc file for it to work&#8230;.don&#8217;t ask&#8230; :oP