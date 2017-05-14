---
layout: post
title: Bypassing Instagram Email Verification System
---

---

#### Description 

It is similar to the <a href="/2014/09/08/bypass-email-oculus/">Oculus Email Verification Bypass</a> vulnerability I reported except that it only involved of changing attacker's own email address for a couple of times
and generating a new secret-token to the attacker's own email inbox.

Yeah, and some Base-64 magics too. (not anything exciting!)

Next step is to change the email address to target's email address. It sends a verification token to his account,which the attacker can't access. 

But attacker then uses initially generated tokens to successfully verify target's email address on his Instagram account.

What's less exciting about this bug comparing to the <a href="/2014/09/08/bypass-email-oculus/">previous one</a> is that it only allowed to use someone's email address to create an Instagram account and verify it which definitely annoys the target,but never causes any harm in depth. Yet, Facebook rewarded this bug with a generous bounty.


{% highlight text %} 
Report sent : 22 Feb 2015 
Escalation : Never notified
Fix : 17 March 2015 
Bounty awarded : 18 March 2015 
{% endhighlight %}

Hope you enjoyed reading it!

