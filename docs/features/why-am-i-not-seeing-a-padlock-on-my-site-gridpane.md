# Why am I not seeing a padlock on my site? | GridPane

# Why am I not seeing a padlock on my site?

 

1 min readWhen you visit your site, if you have SSL toggled on, you should see a padlock next to the URL:

If you don’t and see this instead:

It means you have mixed content on your site, you have most of the assets loading via SSL, but you’ll have some not loading via SSL.

A great resource for determining why this is happening is:

https://www.whynopadlock.com/

Sometimes WhyNoPadlock doesn’t pick up on the error if it is a slow loading asset. In that case you can also use Google Console:

You would see something like the below message:

The solution to this issue is to change links the http to https.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

