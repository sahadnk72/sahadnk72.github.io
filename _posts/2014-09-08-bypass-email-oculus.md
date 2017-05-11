---
layout: post
title: Bypassing Oculus Email Verification System and Gaining Account Access
---

---

We all have seen many kind of verification processes while starting an account with most web applications.The most common form of verification method is either through email address or phone number or a mix of the both.

This post demonstrates how I bypassed the email address verification system implemented for Oculus, a Facebook acquisition. Normally, abusing this kind of vulnerabilities, attackers can use anyone's email address to create an account,which stops the original owner from creating an account since the email address is already taken.

<b>But here, the case was even worse</b>. Oculus developer platform worked in a different way. Since companies could register for an account, it recognized company's domain-name from the email address and added every user account created with a 
company's domain-name,to the company's account as members. Bang!!

For eg: Suppose xCompany has it's email address as `official@xcompany.com` and they uses it to register a company account. Now the admin can add users into the dashboard.

Also, any user who registers for a normal account with their employee email for eg:, `alice@xcompany.com` would be automatically added to the company account as a member.

For all of the things mentioned above to happen,the users should verify their email address by clicking on a verification link received to mail inbox.

What if an attacker manages to bypass the verification system?

He can create an account/replace existing email with target's email address(`attacker@xcompany.com`) and can end up being a member of the developer team for xCompany.

#### Description


I've encountered it multiple times that some web-applications accepts the same secret-token or verification-code on multiple endpoints.To be more specific, when we request for a password recovery, a password reset token is sent 
to our email address.Consider the link received through email looks like this:

`https://developer.oculusvr.com/pass-reset?token=6dd53acf465aa5fbb91ba2a6c7f7`

Then there is a chance that the same token (`6dd53acf465aa5fbb91ba2a6c7f7`) gets accepted for email verification too, for eg:

`https://developer.oculusvr.com/email-verify?token=6dd53acf465aa5fbb91ba2a6c7f7`


#### How it works


Step 1 : Attacker creates an account with his own email address (for eg,`attacker@gmail.com`)

Step 2 : Attacker verifies the email address by clicking on the email verification link received to his inbox.

Step 3 : Attacker requests for a password recovery link for his account and extracts the token received. Let's call it `passtoken`.

Step 4 : Attacker goes on and edits the account settings to change his email to an email address with target's domain name (`attacker@xcompany.com`) which sends an email verification link (with `verifytoken`)to that email address which doesn't even exist.

Step 5 : Attacker uses the initially extracted token (`passtoken`) on email-verify endpoint and circumvents the protection and ends up being a member of `xCompany`. Profit!!


It worked because,both the `passtoken` and `verifytoken` were still valid for his account, and the application failed to validate/differentiate it's purpose. 


{% highlight text %} 
Report sent : 28 Aug 2014 
Escalation : 29 Aug 2014 
Fix : 07 September 2014 
Bounty awarded : 08 September 2014 
{% endhighlight %}

Hope you enjoyed reading it!
