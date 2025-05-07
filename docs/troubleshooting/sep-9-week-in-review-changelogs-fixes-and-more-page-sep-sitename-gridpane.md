# Sep 9: Week in Review - Changelogs, Fixes and More! %%page%% %%sep%% %%sitename%% | GridPane

# Last Week in Review: Changelogs, Fixes and More!

 

5 min read#### 

#### Week of 9/9/19 – SSH Auth Changes, Squashed a New Account Bug, and Other Security Patches!

Per our introduction post, one of the areas that we know we can do better on is with Changelogs. In fact, this is an area a lot of SaaS companies struggle with – so we’re trying to do better. While we don’t have SemVer numbers for our changes, we think anything is better than nothing.

Without further ado, let’s dig into it. This week we see a lot of great changes landing in the release today. Most of these items are only hitting production in today’s release. However, some of these trickled out as host fixes over the past week.

#### A Cut Above the Rest: A Few Changes Worth Noting!

#### A great disturbance in the force…

Recently things have been running pretty well around here. Too well – and without pause reality came knocking. Long story short, this week we ran into two issues that we needed to address.

First, we recently realized that there was a security flaw in how we manage system users. This is an area we’re sensitive to as we try to go above an beyond for security concerns. Something we felt we were doing right when competitors were not. After realizing our mistake we quickly adjusted to fix the issue. As such, SSH Password Authentication is now properly and fully disabled on all GridPane servers.

The next thing was a minor snafu with account creation/upgrade that some of you may have noticed. This issue would have prevented users from signing up (or upgrading) to one of our Paid plans. Not an idea situation! After debugging the issue we traced it down to a bug with our payment processing and then fixed it up!

#### All of the Changes! (The rest of the changes)

#### What’s Up Next?

In the coming weeks we expect to roll out even more important changes. From a support perspective, we’re hoping to migrate from Intercom to Zendesk. We’ve backed up everything from our end, but it may be wise to make your own backup of support cases from Intercom.

On the security front, we’re looking into what we can do about our older Plaid stack. This is a platform that’s been effectively deprecated. Our Dev team is not doing any continued development on that platform and it is not getting new features or improvements. We will eventually be deploying improved tools to help migrate from Plaid to Prometheus. Once that happens we will officially be announcing the EOL for Plaid.

Finally, on the platform side of things we’ll continue to be making steadfast improvements. We’re still constantly taking your feedback from real support cases to drive our priorities here. Some areas we’re focusing on to note are: Teams, the Domains manager, and DNS management. You can expect to see some changes to all these in the near future.

Until next time, from the GridPane Dev team, have a great day!

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

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

 

 