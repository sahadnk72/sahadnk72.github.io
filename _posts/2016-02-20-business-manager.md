---
layout: post
title: Facebook Business Manager Email Address Verification Bypass
---

---

#### Description

When a <a href="https://business.facebook.com">Business Manager</a> user decides to change his/her business email under user settings, they should verify the email ownership by clicking on a link sent to that email. 
This verification procedure is to prevent abuse.

I found it possible to cicumvent this feature to add any business email address without verification.

#### Reproduction:

1. Authenticate into Business Manager.

2. Go to Business settings --> People.

3. Edit the email address of say, admin to any address.

4. Capture the request using any intercepting proxy and edit the value of parameter `email` to the target business' email and edit the value of parameter `pending_email` to attacker's own email address.

5. Complete the request and reload the page.

New email address was added bypassing the verification process.


{% highlight text %} 
Report sent : 04 Dec 2015 
{% endhighlight %}

It was deemed as a duplicate report by Facebook security team.Thanks for reading!

