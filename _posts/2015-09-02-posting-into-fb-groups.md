---
layout: post
title: Bypassing Instagram Email Verification System
---

---

#### Description

Update : It is found that this bug was already reported by <a href="http://philippeharewood.com/the-group-idphotos-endpoint-isnt-obeying-the-publish_actions-and-user_groups-permission-requirement/">Philippe Harewood</a> and fixed by Facebook 
even before my report. This is another example to understand how code changes might have caused the same vulnerability to reappear.



According to Facebook's Graph API documentation,publishing through photos edge of groups other than 'App and Games groups' needs `publish_actions` permission and either `user_managed_groups` or `user_groups permission`.

It was found possible to publish through this edge,without using `user_managed_groups` or `user_groups permissions`, but only `publish_actions` 

#### Worst part:

It posts an update to the attacker targeted group (ofcourse, victim should be a member of) EVEN if the user had only granted 'ONLY ME' privacy mode for posts while allowing the access token.

#### Reproduction:


1.Get an access_token from a test account with `publish_actions` scope set.

2.Using Graph Explorer, make a post on behalf of the user to the 'photos' edge of the node {group-id}.

2.Use the POST field `url` and point it an image url.

3.Complete the request.

It returns an id and post_id after posting the update.

{% highlight text %} 
Report sent : 22 Feb 2015 
Escalation : Never notified
Fix : 17 March 2015 
Bounty awarded : 18 March 2015 
{% endhighlight %}

Thanks for reading!

