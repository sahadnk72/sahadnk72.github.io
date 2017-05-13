---
layout: post
title: Bypassing Instagram Email Verification System
---

---

#### Description

<i>Update : It is found that this bug was already reported by <a href="http://philippeharewood.com/the-group-idphotos-endpoint-isnt-obeying-the-publish_actions-and-user_groups-permission-requirement/">Philippe Harewood</a> and fixed by Facebook 
even before my report. This is another example to understand how code changes must have caused the same vulnerability to reappear.</i>





According to Facebook's Graph API documentation about <a href="https://developers.facebook.com/docs/graph-api/reference/v2.9/group/feed">publishing to groups</a> other than 'App and Games groups' needs `publish_actions` permission and either `user_managed_groups` or `user_groups` permission.

It was found possible to publish through the `photos` edge without setting `user_managed_groups` or `user_groups` scope, but only `publish_actions` in the access_token. 

#### Worst part:

It posts an update to the attacker targeted group (ofcourse, victim should be a member of) EVEN if the user had only granted 'ONLY ME' privacy mode for posts while allowing the access token.

#### Reproduction:


1.Get an access_token from a test account with `publish_actions` scope set.

2.Using Graph Explorer, make a post on behalf of the user to the 'photos' edge of the node {group-id}.

2.Use the POST field `url` and point it an image url.

3.Complete the request.

It returns an id and post_id after posting the update.

{% highlight text %} 
Report sent : 02 Sep 2015 
Escalation : 22 Sep 2015 
Fix : Fixed sometime after rewarding the bounty.
Bounty awarded : 04 May 2015 
{% endhighlight %}

Thanks for reading!

