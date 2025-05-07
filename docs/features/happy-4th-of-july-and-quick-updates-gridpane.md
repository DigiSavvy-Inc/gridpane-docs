# Happy 4th of July and Quick Updates | GridPane

# Happy 4th of July and Quick Updates

 

6 min read

Happy 4th of July (for tomorrow) everyone! We hope you have a great weekend.

### Transcription

What’s up GridPane family. It is Friday, July 3rd. For those of you that are not working right now, enjoy your time off, enjoy your weekend. If you are working, hustle, hustle, get that stuff done so that you can hopefully go and enjoy what we have here anyway, which is a beautiful day.

I put a quick poll in the group to see if people wanted us to go ahead and push a bunch of updates, which we then would not be able to support because we are going to be off for the 4th of July holiday. Everybody pretty much responded with a resounding “definitely don’t do that. Enjoy the weekend”. So we’re not going to be pushing an update, but I figured I would run through what is in the update so that you guys will know what’s coming on Monday.

So real quick, one big thing that we’re doing is new automatic, generated system users with every new site. We’re doing this for security reasons, but we’re also doing it in order to be able to monitor performance and system utilization by individual sites. If every single site has its own system user, then you’re going to know a lot better which site is chewing up your entire box. For developers, you’re going to see the option to build Maria DB 10.5.

MariaDB 10.5 will be an option for you during search server provisioning

We’ve added in Oauth and currently that’s available via a Gitlab and Github. We’re not starting with Twitter and Facebook and all these other places, as places like Cambridge Analytica made it so that we can’t have nice things. It’s just a total pain in the ass to do that stuff. And I figure if you’re in serious developer mode, then you’re already in Gitlab and Github anyway, and then you can jump right into a GridPane.

When you do site migrations, clones, failover all that stuff, the system user that you have the site running on, that’ll be cloned over as well. and with that whatever routing you have (www or root) that routing also gets copied over.

>We’ve got some reduced payloads for server creation which has beneficial for API users, which is not all of you. It’s not many of you actually, but, we’ll talk more about that one later.

Various bug fixes, we’ve got some team bug fixes where admins couldn’t delete system or their own team members – that’s fixed, auto SSLs with alias domains. They were still showing on even if the primary domain failed.

We fixed that domain routing. There was a bug wherein certain instances if you switched to www or rude, and then you made other changes, those things where we’re switching back to, to set on verified users, not being able to log in that’s fixed console errors during server deletions fixed on new feature, all new servers are being built with Monit 5.2 0.6. and we’re including a slew of new notifications and system utilization checks. So if you get anywhere near 70% or more on RAM, disk, CPU. You’re going to start like basically the backend of the application itself and your Slack notifications are going to light up like a Christmas tree. So we shouldn’t have any more situations where maybe your backups fill up your drive, or for whatever reason you haven’t been tracking, how much CPU utilization or Ram utilization you’re going to know about those things a lot sooner now, a PHP workers are now set dynamic based on core count. We’re going on the low end, two times core count, two at most four times core count, and we’re going to be releasing documentation and sort of some like default standards that you can choose based upon the specific use case that your site falls under, based on his traffic profiles, et cetera.

We’ve done some new rewrites within the robot’s text. So for like a virtual rewrite that SEO press does and similar plugins, we’ve completely enhanced the cert about renewal checks. And we built in some self-healing for the Acme SSL configs. Some improvements there and some bug fixes migrations, clones, backups, restore staging. If you’ve had any bugs with those functions and you had manually changed the WP config, if you’ve done like nonstandard stuff where you had, you were using double quotes in one line and single quotes in another line, if you changed any of our default configurations and you had things failing, we now have all kinds of traps and locks and checks, so that those things shouldn’t happen. Even if you’ve monkeyed around with WP config and sort of saved things in a way that you maybe shouldn’t have. And now we’ve also got to fix where fail oversights that were not showing up correctly. They’re not showing up correctly in sites that are not failovers that we’re showing up as failover, that’s fixed as well.

So, a slew a different bug fixes, lots of little things going in, but then also some, some significant improvements with the new monitoring, new notifications, new Maria DB. And we will demo those things Monday, Tuesday of next week. And you’ll see them in the platform.

So hope you all have a safe week.

And again, we’re on critical support only now through Monday. So try not to do anything to break your sites. Certainly if anything happens, we’re here, you know, we’re here 24 seven, but we’re trying to enjoy this weekend as well. So just please be mindful of that and please be patient with us and, yeah. Thanks for your time. Everybody take care, stay safe. Happy holidays if you’re celebrating happy weekend, regardless. Cheers.

### Upcoming Updates

And here are the coming updates in a list for y’all: –

 

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

 

 