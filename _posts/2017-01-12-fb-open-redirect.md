---
layout: post
title: Unvalidated URL Redirect - Facebook Bug Bounty
---

---

#### Description

An open redirector requires no explanation. Unvalidated redirects and forwards are possible when a web application 
accepts untrusted input that could cause the web application to redirect the request to a URL contained within untrusted input <b>[OWASP]</b>.

I found that the GET parameter named `groupuri` at the endpoint `https://www.facebook.com/browsegroups/addcover/log` could be manipulated to achieve
url redirections to external websites. It disallowed direct injection of external links and any suspicious activity would cause a redirection to /home.php.
So I abused the URL shortening feature `fb.me`. It had some black-list based validations to ensure that no redirections are permitted towards existing `fb.me` service domains 
such as `d.fb.me` , `on.fb.me`, `www.fb.me` and `fb.me`.
After some fuzzing and playing around with the parameter `groupuri`, I tried if arbitrary subdomains of fb.me (for eg: `dfHDKJFHjdhf.fb.me`) except the ones mentioned above would work and VOILAAA...a 302.
I was able to shorten an external url using fb.me and tried if it would make redirections if a request is made to any arbitrary sub-domain of fb.me. That worked and I proceeded onto writing a cool report. 
What happened here is, instead of using a regex based validation technique, Facebook relied up on a black-listed based approach. 

{% highlight text %}
Reported - Dec 15 2016 
Clarification sent - Dec 16 2016
Fix - 11 Jan 2017
Bounty - 19 Jan 2017
{% endhighlight %}

Thanks for reading!
