---
layout: post
title: Page moderator can change timeline visibility - Facebook Bug 
---

---


#### Description:

It was possible for a page moderator with Facebook Messenger access_token to change timeline visibility of a post by issuing a request to the following graph endpoint after setting proper values.



`https://graph.facebook.com/v2.2/<PAGE-ID>_<POST-ID>?access_token=<MESSENGER-ACCESS-TOKEN>&timeline_visibility=hidden&method=post`

The GET parameter `timeline_visibility` can have any of these values: `hidden`, `normal` or `starred`. 

According to <a href="https://www.facebook.com/help/323502271070625/" target=_blank>Page Role specifications</a>, it should not have happened. 

 
Upon successful request, the timeline visibility of the particular post changed into whatever state was passed through that parameter.


{% highlight text %} 
Report sent : 27 July 2015 
{% endhighlight %}



Facebook responded saying that it was a duplicate of an issue they were already tracking. Thanks for reading!
