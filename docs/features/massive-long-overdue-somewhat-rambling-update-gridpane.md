# Massive, Long Overdue, Somewhat Rambling Update… | GridPane

# Massive, Long Overdue, Somewhat Rambling Update…

 

9 min read
![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1023'%20height='683'%20viewBox='0%200%201023%20683'%3E%3C/svg%3E)

I’m gonna be covering a lot of ground here, as efficiently as possible. And so a TL;DR isn’t really feasible.The most important thing that I want everyone to get out of this is that we’re doubling down on our commitment to this community, to every single one of you.And the proof in the pudding is in the very last section around what is going to come next with our upcoming plans.

There are four main topics that I want to cover that largely center around some of our shortcomings and the inevitable erosion of confidence in what we’re trying to build here.

1.) Delays on “Beta” Projects

2.) Status of Trainings and Why I’m Even Doing Them

3.) Better Communication/Schedules

4.) Making Changes to the Platform Based on ALL of Your Feedback

So here we go…

## 1.) Delays on “Beta” Projects

We’ve jumped the gun so many times now that it’s broken some hard-earned trust from some within our community, particularly from those who have been waiting the longest.

We always do our best to not only meet but exceed expectations, but when it comes to timelines we’ve had a rough go of it.

Unfortunately, the development time for many features has proven impossible to accurately estimate. Sometimes we have to shift gears entirely from development to maintenance as the providers that we integrate make updates etc.Other times, an aspect of a planned feature reveals a hidden need that is significantly more complex to implement than the original feature.This has particularly been the case with 360, where the billing components were roughly five times more complex than the core monitoring and alerting functions themselves.All of this has the potential to prolong feature releases in ways that aren’t predictable.I want to specifically address Backups V2 and OLS because they’re the main “Beta” features that people are waiting on.

V2 backups, in particular, has taken much, much longer than we had ever anticipated or were able to foresee. Primarily because we keep adding to what we believe is the RIGHT way to do them.If I could go back in time, I likely would go with a much simpler route, but ultimately everyone on GridPane will benefit from what will be one of, if not THE, most comprehensive backup systems available anywhere.

Rest assured that we want this in production just as much as everyone in the community. But it’s important to note that the way we define Beta is not necessarily the same as what everyone assumes to be the case.We’ve continued to add more and more features into V2, pushing new updates nearly every single month. With every new improvement comes the possibility that we’ve introduced a new bug. Hence the “Beta” label.

When Google finally made Gmail “production” it was more than five years after its release. Chrome was in beta for only 14 weeks. I would argue that Chrome today is less stable than GMail was in 2009.And I would also argue that our V2 backups are more stable than all kinds of other options – including V1 – that have been “not beta” for years.

OpenLiteSpeed being in “Beta” is a different situation entirely: OLS itself introduces bugs into “production” which we then have to identify and actively patch based on extensive testing. Testing which is incredibly tedious because they have no standard error mechanisms with certain kinds of errors. Documentation for OLS is also nonexistent, so we need to create it all from scratch. Both for our internal use, to train our Nginx team members, and for the wider public.

We have some of the foremost experts in the entire OLS ecosystem working on our implementation, and I’m similarly confident that it is no less stable than other platforms out there.Regardless of how anyone is labeling their release.

## 2.) Status of Trainings and Why I’m Even Doing Them

There have also been some rumblings recently around delays in training releases and/or some version of: “Why are you even doing THAT instead of working on the stack, V2 backups, or [INSERT FEATURE I WANT MOST RIGHT NOW]?!”Lemme address the second part first:

I’m literally the last person in our entire company that should be working on features, stack, application, support, or any of the technical aspects.There are more than 15 other people FAR more qualified than me to be working on all of those technical issues. The engineers working on the stack and the app make me look like a mouth-breathing buffoon by comparison.My job is to keep the lights on and find the right team members for all the myriad jobs.

When I’m not selling, recruiting, or trying to facilitate our team, I find time to create courses that I think will add value to our community and which complement the extensive documentation which we’ve created.

Delays, case in point: Infinite Infrastructure.The short version is: I’m the constraint in the context of training, always. And trainings unfortunately always have to take a back seat to every other fire.With Infinite Infrastructure I first had hardware failures, which were then compounded with COVID scares at home and me having to quarantine with the kids, which meant the final few video edits and landing page polish weren’t possible and this delayed the release a couple of times in a row.

I’m happy to say that the course is now live. If you would like to learn more about this you can see what it’s all about here:

https://iaas.wtf

Starting with this course going forward we’re going to change how we’re doing things:

Rolling releases don’t work because more pressing fires take precedence over them. In the case of HostingMBA our objective was to release three to four more modules leading up to a live event… which we now don’t even know if we can pull together, due to continued global complications with COVID.

So now all of that effort and investment will be channeled into simply completing all outstanding modules, from all courses, on a highly accelerated timetable.

Additional training has already been added to the HostingMBA and an additional three modules are in final edits now. We expect the bulk of all outstanding training to be released before the end of the month.

Enrolled students will get updated timelines starting the week of September 13th.

## 3.) Better Communication/Schedules

Moving forward (starting in October), Steve will be publishing a “GridPane News and Last Month in Review” update to the blog within the first week of each month. We’ll send an email to everyone via email and post a link to it in the Facebook group and Community Forum.We’re also going to be holding multiple office hours/water coolers/happy hours, multiple times each month including, whether you like it or not, yours truly.I’m also going to reboot my efforts on the YouTube channel and our blog.I don’t want to over-promise on any of these things, so I’m going to simply ask that you be patient and you watch what rolls out in the days and weeks to come.Let that be your barometer of what you can expect going forward.Note: the recent “marketing machine” narrative didn’t make a whole lot of sense to me at first because we literally send roughly one email every other month. If that.The lightbulb moment came when I realized that we basically only email to announce new offerings. We don’t send emails to say “Look at changelog!” or “Look who we hired!” or “Look at this cool new thing!” And we should.So, yeah, fair call. Not a great look. Entirely on me.So we will fix that. Starting today.

## 4.) Making Changes to the Platform Based on ALL of Your Feedback

In the past, we’ve incorrectly made decisions around features, changes, and pricing without direct feedback from many of you. Or, in some cases, no feedback from ANY of you.Which is pretty daft.We should have done a much better job letting the community help shape our direction.  This was a pretty big mistake on my part.So our objective over the next 60 days is to contact and/or directly speak with each and every single active account and get your honest feedback (good, bad, and ugly) in a few areas if you’re willing to share.

From our initial emails and questions, we’re going to follow up individually with one-on-one Zoom meetings, if you’re willing.Some of you may remember our lengthy discovery calls back in 2019, this will be similar to that.

We’re going to take a cross-section of all those responses – some of it completely at random – but mostly weighted around account tenure and tier, and we’re going to change things. We’re going to get better.

Not everyone will get exactly what they want, of course.We’re never gonna do email, sorry/not sorry!But ALL of you who want to be heard and all of you who want to be part of what comes next, you will have that option.

Keep in mind this means we have to contact, on average, dozens of people per day, for 60 straight days. So, that means:You might get an email on a weekend.You might get an email from me.You might get an email from a team member you’ve not met before.You might get an email from a member of our advisory board.Regardless, this will take time. Please be patient, we will definitely get to you.But, if you want to jump the line and get in the priority queue, you can do that by filling out the form at the link below.Note: You don’t have to fill out the form, we will still be reaching out to you, but if you want to move to the front of the line you can do that with this form.

https://forms.gle/GfcMZS1a5J1WBajEA

We look forward to speaking with and catching up with each of you in the near future!

 

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

 

 