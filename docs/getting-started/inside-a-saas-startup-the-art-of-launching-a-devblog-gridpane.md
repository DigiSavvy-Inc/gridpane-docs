# Inside a SaaS Startup: The Art of Launching a Devblog | GridPane

# Inside a SaaS Startup: The Art of Launching a Devblog

 

5 min read 

### Hello world! I am Dev, welcome to our DevBlog

Today is the dawn of a new day on the GridPane blog.

This post is the first of many to come directly from the GridPane Dev team. The hope I have for this is that we’ll be able to close an invaluable feedback loop with you guys. We always get great suggestions (ideas, bug fixes, feature requests, etc) from our customers. So it’s time we share some of that love back with the community!

#### Ingredients for a Successful DevBlog

This section will be brief – the ingredients for success in our case will be what matters most to our community. From our experience it often comes down to a few simple things; being honest, having open communication, having customer-driven priorities, and “owning it” if and when inevitable mistakes happen.

Here’s what you can expect:

Anyway – the point I was making – this blog is us at GridPane doing what we can to complete that feedback loop. You guys give us a lot of good stuff, so now I will be giving some of that back.

So to give you some more ‘concrete’ proof of what’s to come…I’m going to tell you about a feature everyone loves to hate until they need them – Backups. Just imagine this next section was from a future post.

### People don’t want backups, they want restore

On the theme of owning it – recently we had to disable remote backups as the current implementation is causing some issues. In truth, for some customers, we even see some load issues for local backups as well.

After joining the team, one of my first tasks/projects has been to work on a fix for these areas. So currently my focus is finding us the right solution that can be a drop-in replacement and set us up for new functionality later.

My priorities here are finding a solution that’s: a) efficient with load related resources, b) efficient with storage space, and c) based on modern systems (if possible). It can’t be overstated that this blog contains preview information that can change at any time – that’s part of this new dynamic I’m building here. 😄

The solution I’m looking at hits all the marks so far. It’s fast, secure and verifiable. Backups that take too much time aren’t used, so aren’t there when you need.

I looked for a tool that would only be limited by network/disk bandwidth. We don’t want something fast, but brutal – so it can de-duplicate before it actually writes to storage. Security is always critical – so the solution assumes lack of trust and will encrypt the backups.

And finally, what’s more important than backups is that you can restore them. Specifically, it matters that you can verify this without needing to restore them. The solution provides means to verify all data is restorable, accessible and safe.

Once I’m more confident in this path forward – after more scenario testing – I will reveal more details. Until then, know that – if I’m not helping you on our Support, then – I’m working on this! And constantly using your feedback to drive me to the right solution.

### Your Feedback, It Matters and we are always listening!

###### Don’t worry, we’re not always listening like Alexa though.

Your feedback and input is valuable to us and I want a way for us to show you how. Not only that, but to pull back the curtain a bit and show you guys what we’re working up. For instance I’m looking forward to expanding on the backups projects as I make more progress in the weeks to come! I know getting our native Remote Backups back and is a hot topic for a lot of you.

Starting last week – anytime I saw something in our Support Desk that was about features, bugs, or similar I logged it. I’ll be using this log to help me curate the content for this blog and ensure our Dev team is prioritizing things correctly.

### Closing the Feedback Loop…

So – this was a lot – let’s do a quick recap. Whatever crosses our support desk – that falls in this area – will end up on my list. Then as I work to create these blogs I’ll use those items to drive my process. I may be the DJ at this party, but you guys are all picking the tracks!

So I invite you to come join us on this, IMHO, exciting journey and we continue to build and grow our amazing platform. Sign-up for the DevBlog mailing list today!

 

 

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

 

 