---
layout: post
title: Page moderator can change timeline visibility - Facebook Bug 
---

---


#### Description

It was possible for a page moderator with Facebook Messenger access_token to change Page timeline visibility by issuing a request to the following Graph endpoint after setting proper values.



`https://graph.facebook.com/v2.2/<PAGE-ID>_<POST-ID>?access_token=<MESSENGER-ACCESS-TOKEN>&timeline_visibility=hidden&method=post`



The GET parameter `timeline_visibility` can have any of these values: `hidden`, `normal` or `starred`.  


Upon successful request, the timeline visibility of the particular post changed into whatever state was passed through that parameter.


{% highlight text %} 
Report sent : 27 July 2015 
{% endhighlight %}



Facebook responded saying that it was a duplicate of an issue they were already tracking. Thanks for reading!
