---
layout: post
title: Posting videos into Pages when admin disallow
---

---


It is possible for public audience to post contents including photos,videos etc. into a Facebook page if admin allows such 
activities through their Page settings.
There is an option for admin to disable posting of `photos and videos` in Page settings. While checking for access control issues, 
I found that page analyst could still post video even though admin disallows it. It was not possible to post photos or 
text updates,but I could successfully post a video through the graph API using Analyst's access_token with `publish_actions` scope.

{% highlight text %} 
Report sent : 31 Mar 2015 
Escalation : 31 Mar 2015 
Fix : 06 April 2015 
Bounty awarded : 06 April 2015 
{% endhighlight %}

Hope you enjoyed reading it!
