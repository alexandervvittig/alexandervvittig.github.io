---
id: 555
title: Getting started with Python
date: 2016-09-25T14:33:48+00:00
author: Alex W
layout: post
guid: http://blog.vvittig.com/?p=555
permalink: /2016/09/25/getting-started-with-python/
categories:
  - Python
---
  1. Install Python 2 ( download it from [here](http://python.org/download) )
  
    [See bottom notes about why **Python 2**, not 3].
  2. Open PowerShell and type _python_
  3. If you get an error define the environment variable to know about python <pre class="lang:ps decode:true ">[ENVIRONMENT]::SETENVIRONMENTVARIABLE("PATH", "$ENV:PATH;C:\PYTHON27", "USER")</pre>
    
    Close PowerShell and open it again and try _python_ again.
    
    If done right, you should see something like this:
  
    [<img class="aligncenter wp-image-556" src="http://blog.vvittig.com/wp-content/uploads/2016/09/python-300x52.png" alt="python" width="600" height="105" srcset="https://blog.vvittig.com/wp-content/uploads/2016/09/python-300x52.png 300w, https://blog.vvittig.com/wp-content/uploads/2016/09/python-768x134.png 768w, https://blog.vvittig.com/wp-content/uploads/2016/09/python.png 789w" sizes="(max-width: 600px) 100vw, 600px" />](http://blog.vvittig.com/wp-content/uploads/2016/09/python.png)Hooray, we have Python 2 now installed.
  
    To exit Python you can type _exit()_</li> </ol> 
    
    Note: Why Python 2 vs Python 3 to get started:
    
    > A programmer may try to get you to install Python 3 and learn that. Say, &#8220;When all of the Python code on your computer is Python 3, then I&#8217;ll try to learn it.&#8221; That should keep them busy for about 10 years. I repeat, _do not use Python 3_. Python 3 is not used very much, and if you learn Python 2 you can easily learn Python 3 when you need it. If you learn Python 3 then you&#8217;ll still have to learn Python 2 to get anything done. Just learn Python 2 and ignore people saying Python 3 is the future.
    
    Source: <https://learnpythonthehardway.org>