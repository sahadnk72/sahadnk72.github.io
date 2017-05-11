

#### Description

  This post is about a simple bug I found in Facebook which allowed me to chat with any minor,even if they are not in our friendslist.
It was a privacy issue where a user could send messages to a minor who was a total stranger when they shouldn't be able to do so.

According to Facebook,
Minors can receive messages only from people who are friends of friends and people who have their contact information (ex: email address or phone number). This may include adults they don’t know.

But there I found a bug which was very easy to find and exploit to circumvent this security feature.

For a minor who have changed his/her message preferences from Basic Filtering to Strict Filtering (for more privacy)
in privacy settings,this trick worked.

First of all we need to extract the target's profile id.

Do a graph check to get  fbid.

`http://graph.facebook.com/victim`

Visit 

`https://www.facebook.com/messages/<FBID>`

Name of the minor appeared in the field "To:"
I sent a "hi" without seeing any error as usual. Yes, that was it. Sometimes the bug finds us before we get to them.
Then I logged in to the target's account to check if the message was received and found it was showing up right in their inbox.

Issue was fixed and rewarded me a bounty after it was reported to the security team.

Thanks for reading!
