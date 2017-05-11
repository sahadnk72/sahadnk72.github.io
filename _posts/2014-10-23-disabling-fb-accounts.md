---
layout: post
title: Disabling any unverified accounts - Facebook Bug
---

---

When a new Facebook account is created a verification code is sent to the email of the user to confirm their identity. Email contains an option to disavow the confirmation link in case the email was misused or used by someone else to create an account.

The link behind {% highlight text %}Didn't sign up for Facebook?{% endhighlight %} had a confirmation code in it, which was a 5 digit code :



`https://www.facebook.com/confirmemail.php?e=EMAIL_ID&c=5-DIGIT-CODE&report=1`


The parameter `c` could be brute-forced by an attacker to find the right confirmation code and disable someone's unverified Facebook account. 

Facebook fixed this after it was reported to the security team.


{% highlight text %}
Report sent : 29 Aug 2014
Escalation : 29 Aug 2014
Fix : 23 October 2014
Bounty awarded : 23 October 2014
{% endhighlight %}
