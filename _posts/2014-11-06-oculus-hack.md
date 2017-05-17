---
layout: post
title: How I hacked into Oculus VR Developer Portal
---

---


Oculus VR - one of the Facebook acquisitions, was vulnerable to many severe issues including RCE, multiple SQL-injections, and a couple of CSRFs.

Many researchers including Jon of Bitquark, Inti De Ceukelaire and Josip Franjković squeezed it to a more secure level. I knew that all the low hanging fruits must had been gone. Nevertheless, I gave it a shot. It is my second finding on Oculus; first was something which allowed me to add anyone's email to an account and verify it without their interaction by crafting a verification link; which led to full account takeover. This one is also somewhat similar, which enabled me to reset random-user's password resulting in successful authentication into their account. Each time I reproduced the request, got access to different accounts, which in turn changed their passwords as well.

I kept trying with many known methods to see if anomaly occurs and that's when I decided to pass query parameters as array instead of string type. This trick used arrays in query parameters to confuse the web application and produce what I really wanted. 

Watch the video!



<iframe width="560" height="315" src="https://www.youtube.com/embed/01a1aProHRU" frameborder="0" allowfullscreen></iframe>


Boom!!


A nice bounty followed up after it was reported to the Facebook security team.


Hope you enjoyed reading and watching!
