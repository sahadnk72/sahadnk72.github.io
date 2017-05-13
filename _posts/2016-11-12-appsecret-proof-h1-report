---
layout: post
title: Leaking Facebook appsecret_proof From a Private Bounty
---

---
#### Description

While analysing the Oauth implementations and authentication procedures for a private bounty target in Hackerone, I found something 
that allowed me to leak the appsecret_proof (`hash_hmac('sha256', app_access_token, app_secret)`) which was submitted to Facebook servers 
from the app server. 

New to appsecret_proof? <a href="https://developers.facebook.com/docs/graph-api/securing-requests">Refer this</a>


While signing into `site.com` using Facebook and intercepting the POST request containing the `access_token` which was being submitted to `https://www.site.com/auth/facebook` after the Oauth flow,
I tried fuzzing the request parameters. I chose to play with the parameter `access_token` and replaced the access_token I just allowed from Facebook with a new access_token I grabbed directly
from the <a href="https://developers.facebook.com/tools/explorer/145634995501895/">Graph API Explorer</a> with minimal permissions. To my surprise, the app didn't validate the response it got from Facebook's
remote servers and passed it on to user end. The error response contained both the `access_token` that was submitted by the user and `appsecret_proof`. Yes, it defeated the whole purpose of using `appsecret_proof`.



Site.com fixed the vulnerability by validating the response they receive from Facebook servers and rewarded me with an awesome bounty ;)

After that, I went ahead and gave Facebook a heads up as there must be hundreds of apps following the same strategy in their implementations. Although it had nothing to do with Facebook, it still had something to do with 
them as throwing the appsecret_proof which the client just submitted,back to them within the error message was pretty unnecessary and something Facebook had
forgotten to validate. Facebook denied to fix the issue stating that it's the client's responsiblity to properly validate the API response and mentioned that those error messages would help in troubleshooting.


Thanks for reading!




