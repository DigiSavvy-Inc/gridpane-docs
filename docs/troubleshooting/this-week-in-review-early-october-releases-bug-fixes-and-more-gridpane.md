# This Week in Review: Early October Releases, Bug Fixes and More! | GridPane

# This Week in Review: Early October Releases, Bug Fixes and More!

 

5 min read#### 

#### Week of 10/4/19 – ZenDesk, Teams Improvements/Fixes, and More Stable Site Builds!

So here we are again friends! This week we see a lot of great changes landing in the release this week. Most of these items are only hitting production in yesterday’s release. However, some of these trickled out as hot fixes over the past week.

Let’s dig in to it!

#### Top Changes for Oct 2019’s First Release

– but you’re good to go with most every other character.

#### Improving Our Support Experience with New Tools

As I teased above, starting yesterday you all will have our new support system in place. Our old tool was a great tool for us getting started – we won’t knock it. Long term though, some of our core goals and use cases didn’t completely fit that system.

Saving the long story about our mission for another post. We strive to provide amazing customer support, so want tools that fit the best for our goals. Our new system should allow for more structured ticketing based support interactions. (So better history access for customers and our admins.)

We’re still solidifying some internal processes and docs around this – expect to see continued improvements. We’re also growing our team slowly but surely, and added a new Support Admin! So we welcome our new team member – you’ll see their name popping up in Chats and Tickets.

#### All the Teams Things!

##### (Less Bugs, More Fixes)

#### A Note on Site Script Stability

On of the peskiest issues we’ve dealt with lately has been failing site builds. And/or site deletions. This would be an issue that would usually not affect a primary site and most often causes stage/canary to fail.

It might be instances where a failed – for some reason – but then clean up after the failed attempt also has an issue. Then subsequent builds fail due to duplicate DB issues. So one half of this issue is the process itself hitting a race condition and not fully executing. Aka, the broken clean up. And the other is, what should happen to better handle this unexpected state. Aka, working past the issue.

So our fix has been to spread out the build process to be slightly less concurrent. This keeps the system more stable and makes the issue state much less likely to occur overall. The other half is that when this is hit, we can now dump the conflicting DB for backup – then, it continue the process.

In a similar permutation of this issue, it can happen when a site is intentionally deleted. During that deletion – in some cases – a race condition could occur causing the site clean up to not fully complete. These cases should be covered in the fix too!

#### Pack It up Folks, It’s Closing Time

So this is our second big release since taking over the DevBlog – maybe I’ll bring cake when I hit 42 release posts? We covered a lot of BIG important changes, there were even more smaller changes in this release too. Those just as important.

Like Default WP Admin improvements (more supported characters), `dns/{site.url}.creds` parsing fixes and more than we can mention.

#### Coming Soon: New Types of Posts

Keep an eye out on your feedburner emails for some new types of content in the weeks to come! Unfortunately this one likely won’t fire off until the day after posting. I missed the trigger deadline – for today – I think. I didn’t want to get to sleep until I knew for sure our customers were going to be set with ZenDesk.

So, IMO, a totally justified tradeoff and completely worth the delay. Sometimes the best things really are worth waiting for.

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

### One comment

## Leave a ReplyCancel Reply

Your email address will not be published. Required fields are marked *

Name  *

Email  *

Website

Please check the box below to consent to the processing of the submitted personal data in accordance with our Privacy Policy, including the transfer of data to the United States.

I have read and accepted the Privacy Policy
		 *

Add Comment *

Post Comment

 

 