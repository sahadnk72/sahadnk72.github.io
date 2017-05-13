---
layout: post
title: Unvalidated URL Redirect - Facebook Bug Bounty
---

---

#### Description

An open redirector requires no explanation. Unvalidated redirects and forwards are possible when a web application 
accepts untrusted input that could cause the web application to redirect the request to a URL contained within untrusted input.
(Source : OWASP)

I found that the GET parameter named `groupuri` at the endpoint `https://www.facebook.com/browsegroups/addcover/log` could be manipulated to achieve
url redirections to external websites. It disallowed direct injection of external links and any suspicious activity would cause a redirection to /home.php.
So I abused the URL shortening feature `fb.me`. It had some black-list based validations to ensure that no redirections are permitted towards existing `fb.me` service domains 
such as `d.fb.me` , `on.fb.me`, `www.fb.me` and `fb.me`.
After some fuzzing and playing around with the parameter `groupuri`, I tried if any arbitrary subdomain of fb.me (for eg: `blah.fb.me`) except the ones mentioned above would work and VOILAAA...a `302` was issued.
After shortening an external url with fb.me, I checked if visiting blah.fb.me would actually make a redirection to the website and fortunately that worked. I proceeded on to making a cool report. So the final url looked like this : 



`https://www.facebook.com/browsegroups/addcover/log/?groupid=1&groupuri=https://<anything>.fb.me/iDent1fi3R`


What happened here is, instead of using a regex based validation technique, Facebook relied up on a black-listed based approach. 

{% highlight text %}
Reported - Dec 15 2016 
Clarification sent - Dec 16 2016
Fix - 11 Jan 2017
Bounty - 19 Jan 2017
{% endhighlight %}

Thanks for reading!
