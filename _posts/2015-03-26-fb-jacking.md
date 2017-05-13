---
layout: post
title: You clicked? You eff'd - Facebook Bug
---

---


#### ClickJacking:


##### According to OWASP: 
Clickjacking, also known as a "UI redress attack", is when an attacker uses multiple transparent or opaque layers to trick a user into clicking on a button or link on another page when they were intending to click on the the top level page. Thus, the attacker is "hijacking" clicks meant for their page and routing them to another page, most likely owned by another application, domain, or both.

Using a similar technique, keystrokes can also be hijacked. With a carefully crafted combination of stylesheets, iframes, and text boxes, a user can be led to believe they are typing in the password to their email or bank account, but are instead typing into an invisible frame controlled by the attacker.

##### According to me:
Clickjacking is an interesting and simple way of exploiting a web application that can lead to serious issues (transfer funds, messaging...). The idea is actually really simple:

We frame a certain website A within an Iframe and using stylesheets, we made it invisible/hidden (when it exists in the background) and reconstruct another site before it. So while you click something on the attacker controlled site, I can actually make you click a button in the framed website.

Owasp have a good example for ClickJacking: For example, imagine an attacker who builds a web site that has a button on it that says "click here for a free iPod". However, on top of that web page, the attacker has loaded an iframe with your mail account, and lined up exactly the "delete all messages" button directly on top of the "free iPod" button. The victim tries to click on the "free iPod" button but instead actually clicked on the invisible "delete all messages" button. In essence, the attacker has `hijacked` the user's click, hence the name `Clickjacking`.


The simplest and effective fix for this is the `X-Frame-Options` header. Even though, Facebook was using one, here is how I bypassed it to make me an attacker do post a status update. :)


#### The Exploit:

The exploit is really simple and effective; Facebook defends click-jacking in 2 ways. One is alternative to the other. They also use a technique called Frame-busting (using javascript to deny framing request). On interfaces which don't have a JS support it is sending XFO, not as a 
HTTP header, but in a meta tag by putting it in a <noscript> tag

`<noscript><meta http-equiv="X-Frame-­Options" content="deny"> </noscript>`

Meta-tags that attempt to apply the X-Frame-Options directive DO NOT WORK. For example, <meta http-equiv="X-Frame-­Options" content="deny">) will not work. You must apply the X-FRAME-OPTIONS directive as HTTP Response Header.


The main point here is browsers ignores what is given in meta tag and do not defend framing, (tested in Firefox 35).

On interfaces which require JS support, it is possible to bypass JS frame-busting by giving a sandbox in the iframe like:

``<iframe id="clickjacking" src="https://iphone.facebook.com/dialog/feed?app_id[APP ID]&picture=http://example.com/example.JPG&name=Test&description=This%20is%20a%20test&redirect_uri=http://example.com/" width="500" height="500" scrolling="no" frameborder="none" sandbox="allow-forms"> </iframe>``

Simple as that, it was possible to iframe Facebook and make you do undesirable amount of things. 
Here is a video demonstrating the seriousness of how this exploit might have been abused:

<iframe width="560" height="315" src="https://www.youtube.com/embed/fGnRA5J0vMU" frameborder="0" allowfullscreen></iframe>


{% highlight text %}
Reported - March 20 2015 
Clarification - March 21 2015
Fix & Bounty  - March 24 2015
{% endhighlight %}


Thanks for reading!
