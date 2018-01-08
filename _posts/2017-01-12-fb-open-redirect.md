---
layout: post
title: Unvalidated URL Redirect - Facebook Bug Bounty
---

---

#### Description


An open redirect requires no explanation. Unvalidated redirects and forwards are possible when a web application 
accepts untrusted input that could cause the web application to redirect the request to a URL contained within untrusted input.


#### PoC

After dorking a lot for old endpoints in Facebook, I found the following endpoint.

`https://www.facebook.com/browsegroups/addcover/log`


It was found to be accepting user inputs through a GET parameter named `groupuri` and the expected value was a URL, to make redirections into the specified URL. I found that it could be manipulated to achieve
URL redirections to external websites. From initial tests it was found to be disallowing any external links to be put through that field. Any suspicious activity would cause a redirection to /home.php.
So I abused Facebook's own URL shortening feature `fb.me`. Even though it had some black-list based validations to ensure that no redirections are permitted towards existing `fb.me` service domains 
such as `d.fb.me` , `on.fb.me`, `www.fb.me` and `fb.me`, I came to see that by simply putting any arbitrary subdomains  of fb.me (which was non-existing : for eg: `blah.fb.me`) would work and `302` was getting issued.
After shortening an external url with fb.me, I checked if visiting the arbitrary subdomain would actually make a redirection to the website and fortunately that worked. I proceeded on to making a cool report. So the final url looked like this : 



`https://www.facebook.com/browsegroups/addcover/log/?groupid=1&groupuri=https://<anything>.fb.me/iDent1fi3R`


What happened here is, instead of using a regex based validation, Facebook relied up on a black-listed based approach. 

{% highlight text %}
Reported - Dec 15 2016 
Clarification sent - Dec 16 2016
Fix - 11 Jan 2017
Bounty - 19 Jan 2017
{% endhighlight %}

Thanks for reading!
