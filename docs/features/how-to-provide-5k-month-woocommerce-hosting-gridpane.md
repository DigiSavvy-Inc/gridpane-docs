# How To Provide $5K/month WooCommerce Hosting | GridPane

# How To Provide $5K/month WooCommerce Hosting

 

13 min read 

 

## A GridPane Client Case Study of a $650K Book Launch

 

Part of what makes providing world-class support so challenging is that everyone thinks that their issue, right now, is an emergency.

See if you can spot the CRITICAL support ticket…

Ticket A: “My site has 5K concurrent users and we’re doing tens of thousands in sales every hour. But the site keeps going down. We’ve got tons of 500 errors. I know we need to scale up but I’m a bit out of my depth on this one. I’ve never dealt with this much traffic before. The URL is whatever.com and the server IP is 1.2.3.4. How should we proceed?”

Ticket B: “My developer (an outsourcer whom I pay less than $5/hour) can’t login. We’ve read ALL the knowledge base articles (we skimmed the headlines) and now I’m wasting all this money. Yes, we’ve tried EACH of those steps (what steps?).”

Ticket C: “I have 273 pictures of Mr. Bojangles in his new outfit, which is adorable BTW. They’re burned to a DVD by the photo place. I don’t have a DVD drive. How do I upload all of these to my site? I’ve opened three other tickets about this same issue over the last ten minutes but no one is answering. IS ANYONE THERE?!?!”

via GIFER

Ticket D: “What’s a ‘WordPress?’” (An investor actually said this to me, verbatim)

We get hundreds of B/C/D level tickets every single day. They create a tremendous amount of noise, and they can make it exceedingly difficult to get through to the A players. So we work tirelessly to refine our processes, our systems, and our team.

What follows is a breakdown of how we handled that exact Ticket A scenario within the last couple weeks. It’s a really good example of the kinds of problems that we want to smash here at GridPane.

And it also serves as a guideline on what you can be charging for your hosting services.

Let’s chop it up…

It was a little after 7PM and I needed to get my girls tucked in. But Tom and Bobby had messaged me directly and they had my complete attention:

A client of ours had over 6,000 concurrent users on his site, with hundreds of people trying to check out in WooCommerce, simultaneously.

For those of you who aren’t experienced with serious traffic events, I’ll give you the hyper-technical breakdown of what that kind of scale we’re talking about here: that’s a metric shit-ton of traffic.

A less formal example: Suppose you write a pithy, entertaining article that trends on a subreddit like “craft beer” and a bunch of people come to your website. At any one time you might have dozens or even 100 people concurrently reading your post. In a single day you might spike to 25,000 total unique visitors.

This, for the vast majority of WordPress sites in the world, is a lot of traffic for a single day.

If you hosted that funny beer article on WPEngine, and continued to sustain that level of traffic for the rest of the month, you would incur an additional $1450 dollars worth of overage fees.

Hopefully all those zingers ultimately help you sell a lot of beer.

This is nearly two orders of magnitude higher than that. Sixty times more traffic. And they’re not just reading, they’re transacting business. A lot of it.

Snap back to reality: I’m reading “Raising Dragons” to a four and six year old and one of our client’s servers is getting hit in the face with a sledgehammer. I let the six year old take the wheel on the book and I pop out to the hall to fire off a handful of quick messages…

I looped in Leo, our Head of Engineering, and he’s already starting to audit things.

I message the support team to confirm I had the full picture. Yes: much sledgehammering-in-the-face, traffic expected to increase.

I messaged the client directly, trying to raise him on Facebook and bring him back into live chat.

He’s busy, for some reason, and I can’t get him. It’s almost like he’s preoccupied with a client of his saying “WTF is going on with my website?!?!”

The entire team is on the case.

There’s nothing for me to do other than wait.

So, back to the dragons book (which slaps, by the way).

Earlier that afternoon someone had sent out a tweet, announcing their new book, to hundreds of thousands of followers. That tweet was the tiny snowball that started the avalanche.

Within just a couple hours it was the top story on CNN.com. Axios and other news sources around the globe were picking up the story. Thousands of people were retweeting the link to the site.

And all that traffic was pointed squarely at: one… tiny… server… hosted at Vultr.

Shit, meet Fan.

Clearly this is the kind of situation that, in a perfect world, you would want to know about in advance and properly prepare for. And, knowing this longtime client of ours, I strongly suspected that he’d been completely blindsided.

Because he would have known better.

Sometimes you can’t control what your clients are going to do.

Like tweeting about the book launch before the book launch is ready to launch launch.

Once we got on the case, everything that needed doing was fairly formulaic:

The sledgehammer would keep coming There was nothing we could do to stop that, not that you would want to. We would simply make the “face” much larger, and put a burly ass helmet on said face.

As soon as we connected with the client, we did our best to shout loudly over all his client noise and get him to tackle #1 and #2 as our hands were tied on those matters. After I put my monsters to sleep, Leo and I connected and started to get a look at this other kind of beast.

The vertical scale-up was somewhat less than graceful because it couldn’t be done “in place.” Vultr has this really daft thing where you can’t scale up very far on their HF line. They have arbitrarily low limits, I suspect for monetization reasons. You’re much more likely to be able to sell a handful of small HF boxes than one or two large HF servers.

So he had to switch to DigitalOcean and their Dedicated CPU droplets. This was less than ideal, for myriad reasons. Not the least of which is that DigitalOcean uses middle-of-the-range clocks (CPUs) across their entire service offering.

But the client needed to staunch the flow of traffic anyway, in order to be able to take a full current backup and get things moved over to the bigger box. So a bit of intentional downtime in this case was acceptable, seeing as though it kept getting knocked down by all the checkouts.

All of this drama could’ve been avoided with proper planning of course. But, again, our client had no warning and couldn’t have possibly foreseen this kind of tsunami. You play the cards you’re dealt.

Once the site came back online there was still work to be done.

Leo took a quick assessment of the new box and immediately switched to static PHP workers, set that count to 50, and just let the checkouts pile into all of that newly available RAM. After a few other adjustments the box was holding stable at about 45% CPU utilization.

No more 500 errors, the WooCommerce checkouts returned to batshit velocity.

## Nerd Tangent #1

It’s important to note here that the problem was not the larger number, the 6K concurrent users, it was the 150+ people trying to checkout simultaneously. With aggressive server side caching, like you’ll find in our stack, thousands of users are carelessly batted away by Nginx, without breaking a sweat. The site was serving the homepage and the book excerpt without trouble.

But once you start a WooCommerce checkout, now you’re talking about hard PHP hits. Which brings us to…

## Nerd Tangent #2

One of the really swell ways that managed WordPress providers bend you over the barrel is by limiting the number of PHP “workers” that you can have access to at any one time. These workers are short-lived instantiations of PHP that do, drumroll please… work.

Prime examples of worker tasks would be the following: “Please check the inventory for this item, if it is available please add it to the shopping cart for this visitor, once they click the checkout button please verify they’ve entered all the required billing information, please ping Stripe and have them whack the customer’s credit card, if everything works out please give the customer a ‘thank you’ message, and then please use the transactional email plugin to fire off the appropriate confirmation emails.”

That’s PHP workers in a nutshell.

Now imagine that all of that “please” and “thank you” business is happening… hundreds of times per minute, as was the case in this situation.

In order to be able to handle the ingestion of all of those tasks, you need the proper stack, the proper configuration, and a sufficient amount of physical hardware to process all of those jobs without falling down.

So back to you and the barrel.

After you get ripped off by…

… the only remaining way to rip you off more completely is by taxing that ass with “workers” limits.

[Throwing Money Spending Money GIF](https://tenor.com/view/throwing-money-spending-money-throw-money-out-of-window-geld-rauswerfen-money-rain-gif-16783981) from [Throwingmoney GIFs](https://tenor.com/search/throwingmoney-gifs)

Well, that’s not the only remaining way actually, because you can rip people off on extra backups, open source software like Redis, open source software like ElasticSearch, formulaic configuration changes like reverse proxy setups, “add-ons” of standard baked-in WordPress functionality like Multisite… and on and and on.

In this case our client bumped up to 16 cores at the “physical hardware” side of things and we kicked PHP to Static and gave him 50 workers. Which is complete overkill for 95% of sites out there, but completely appropriate for this sledgehammer situation.

For a comparable amount of horsepower at Kinsta you’d need three Enterprise 4 accounts plus a Business 1 account, for a grand total of $4600/month.

A similar plan at WPEngine will run you “Call to speak to a sales specialist” dollars.

Which is roughly equivalent to “If you have to ask how much it costs… ”

But in this case, our fearless hero client was able to, in short order, scale their infrastructure and had things properly configured to weather the storm, thanks to our Engineering as a Service team.

All in, he’s looking at less than $500/month, infrastructure included.

## Nerd Tangent #3

Why High Frequency and why is that all the rage these days?

Many Infrastructure as a Service (IaaS) providers are now offering “high frequency” servers. Out of all of our supported providers, Vultr HF is definitely the most popular choice right now. Pound for pound it’s pretty hard to beat that value. I just wish they had a real status page. Regardless of where you get your HF boxes from, the math is the same: faster CPUs are simply able to complete worker tasks faster.

A 3.8Ghz CPU (like you would find with Vultr HF or Google C2) can get much more work done in the same amount of time as a 2Ghz CPU that you might see at DigitalOcean. This improved performance is much more noticeable in WooCommerce or Learning Management System (LMS) contexts because there are just so many more of those hard PHP hits. The faster each task gets processed, the faster the entire checkout or quizzing experience.

Long story long: if you’re running WooCommerce or an LMS or any other transactionally “heavy” workload, and it matters, you should be on a high-frequency option if at all possible.

The following day we took the additional steps of helping them get a completely new, clean, floating IP address at DigitalOcean and we moved their entire setup behind Cloudflare for additional security, load reduction, and – most importantly – Distributed Denial Of Service protection.

For reasons that we don’t need to go into, the DDOS protection was essential in this case. What is worth going into is: make sure that if you’re moving things behind Cloudflare that you still need a totally new IP address because it’s utterly trivial to recover previously cached DNS records and then hammer the shit out of someone’s box directly, circumventing Cloudflare entirely. If one was so inclined.

We kept an eye on things and some final recommendations on their infrastructure scaling going forward. Things remained stable from that point on out, never peaking over 50% utilization, which is a decent rule to live by, if at all possible.

In total, over the course of 72 hours, the site processed roughly $650,000 in sales across 14,000 transactions.

There was stumbling in the beginning, of course, but in the end there was much rejoicing.

I can’t thank the team enough for how this all came together.

And I really want to thank our nameless client for putting their trust in us, to handle this and all their hosting needs.

I largely got to sit back and watch this machine that is GridPane dismantle a serious hosting nightmare with relative ease.

Our tools worked as expected, our team executed well, and the client got their desired results. Namely: they didn’t have to lose sleep over this, because they’ve partnered with a team that wants them to succeed. I think that’s what they wanted. And I believe that’s what we delivered.

We’re not saving the whales or building rockets to Mars, but this whole situation kicked a fair amount of ass.

I like what we do here.

I like the people we do it for.

In the long run, I don’t know exactly what this client will ultimately charge their client for this whole fiasco. But we’ve already seen how others in the managed WordPress space would have priced this all out. And in their defense, $5K a month, or more, for this level of capability, is completely reasonable. Just look at all the upside that their client got in this case.

There’s almost no premium that is too high for the peace of mind that comes from having the right expertise and the right capabilities, at the right time.

That’s what we’re building here at GridPane.

What are YOU building?

If it’s something interesting, and it’s on top of WordPress, we should talk.

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

### 4 Comments

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

 

 