# How and Why We Built Our Knowledge Base on WordPress | GridPane

# How and Why We Built Our Knowledge Base on WordPress

 

15 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1282'%20height='721'%20viewBox='0%200%201282%20721'%3E%3C/svg%3E)

### Table of Contents

 

## Introduction

At the beginning of 2020, we had around 60 knowledge base articles. At the beginning of 2021, we had over 200.

With this rapid expansion of documentation, our publishing needs quickly evolved. In order to provide a better experience for both our clients and our team, we built ourselves a completely custom solution with WordPress.

In this article, we’ll discuss some of the main challenges we faced as our knowledge base grew, how our needs changed, and how we used WordPress to solve the problems we encountered in our previous solution.

 

## Zendesk: Why We Moved

We previously used Zendesk for our support system and this came with its own knowledge base functionality. It was quick and easy to use and their editor is also pretty decent as well. For a simple, small knowledge it’s not a bad solution.

The positives end there though.

Zendesk’s knowledge base functionality is limited in the most bizarre ways and this became a real problem as we poured serious effort into creating comprehensive articles for almost every support ticket that came in that wasn’t already documented.

#### Problem #1

Categorizing knowledge base articles effectively was difficult as we couldn’t add an article to different categories at the same time, which is a serious flaw in their product. Sometimes an article belonged in two or three categories and this is a necessity to ensure our clients can find the information they need as efficiently as possible.

#### Problem #2

Customizing Zendesk for a better user experience was no easy task. The built-in options were limited and we couldn’t display things the way we wanted to.

#### Problem #3

While the search function on the main knowledge base overview page worked very well, the sidebar search bar was completely useless. If you were trying to run a search from the sidebar on an existing article then it wasn’t going to do a good job for the most part. It’s weird and stupid that this didn’t work the same way in both places.

#### Problem #4

Both our platform and documentation were changing rapidly, and the more we grow, the more changes are necessary to keep our documentation up-to-date. We were getting too big to have edit the same content again and again across many different pages and needed a solution that would allow us to make changes to content globally.

Note: Zendesk seems to now offer this in their Enterprise tier but they didn’t at the time.

#### Problem #5

Finally, to top things off, we were receiving none of the SEO benefits that come from our content production efforts as it all stored and indexed on gridpane.zendesk.com. This was a major issue with serious long-term implications.

### Zendesk KB Woes in a Nutshell

The problems we faced with Zendesk’s knowledge base software were that: –

Their knowledge base product lacked basic functionality which had been asked for over and over from their users dating back at least 3 years from what I’d seen in their support threads. It appeared as if they’d made no effort in improving the product in years and it was insufficient for our rapidly growing documentation.

 

## Moving Support Systems

Once the Covid lockdown went global around April 2020 our support tickets went through the roof – a lot of people suddenly had a lot of time to work on their hosting setup and we experienced a 30% increase in support tickets almost overnight. Zendesk is certainly an overall solid support product, but it wasn’t ideal for our own unique needs.

To leave Zendesk meant we had to move to our knowledge base elsewhere anyway, so the timing worked out well and gave us the nudge we needed to prioritize getting everything moved.

Internally we had already discussed building a custom knowledge base directly on WordPress multiple times. Crisp, where we moved to at that time was a chat app, not a full support desk, so we needed a new solution no matter what.

 

## To WordPress! Hurray!

WordPress is an ideal platform to build a custom knowledge base.

Interestingly, a lot of people (even WordPress pros) often look elsewhere when it comes to their knowledge base. Sure, some of the existing solutions out there are fine (I looked at most of them for inspiration while wireframing out ours), but we’re WordPress pro’s so why not take full advantage of what the WordPress ecosystem can offer?

With WordPress, we could customize it any way we wanted, and we can extend it as far as we want in the future. We also get an SEO-ready platform, and our entire team can easily use it.

Whatever we want to create, we can do it easily with WordPress.

Side note: We’ve discussed this topic a couple of times inside the Self-Managed Hosting Facebook group. A great question we got asked in one of those threads was:

 

Doesn’t FreshDesk come with a KB that integrates in with the support? Any reason you decided not to use it?

Having the knowledge base integrated with our support desk would be nice, and we have thought about syncing ours with FreshDesk. However, I think it’s unlikely we’ll do so. It’s rare that a day goes by where we’re not making a tweak here or there to improve things, and it’s not exactly a huge hassle keeping our site open in a tab and pulling links as we need them. If we used FreshDesk as well, we’d be sending people to two different places. That would be confusing, especially for new clients getting to know their way around.

Oh, and we didn’t last long at Crisp. That ended up being a disaster for our support team trying to manage ongoing tickets. We now been using FreshDesk since October 2020 and it has been working out well. It’s far from perfect and it seems no matter what support desk option you choose, you sacrifice some aspects that are great on other platforms for some that aren’t – reporting and analytics in FreshDesk’s case for example are rubbish. So is their internal search.

Our team’s overall workflow is considerably better than on previous platforms though, and that’s the most important thing we need.

 

## Inspiration

“Steal Like An Artist” by Austin Kleon is a great book that I think every designer would benefit from reading. If haven’t already read it, I would highly recommend checking it out.

I wanted to have a clear design in mind first and know exactly what I was building before making any other decisions in regards to software, so I went on the hunt for inspiration. I mentioned earlier that I had looked at most of the knowledge base solutions out there – this is why.

There are some excellent and some very mediocre solutions available, and while this exercise was well worthwhile (I gained some useful ideas which I implemented), nothing I came across that made me think that building it custom in WordPress wasn’t the right way forward.

Along with existing solutions, I looked at knowledge bases from other hosts, popular SaaS companies, and a lot of popular WordPress plugins as well.

I also usually head to Dribbble for a daily dose of inspiration too.

 

## Migrating from Zendesk to WordPress

There’s no way to redirect content inside of Zendesk because of course there isn’t… We had two options here, neither or which was ideal.

The first was to use JavaScript-based redirects and the second was to unpublish all of our content on Zendesk. We went the JS route and, fortunately, this actually went pretty well. It’s definitely not ideal from an SEO or UX standpoint but it did the job and everyone ends up in the right place.

Tobi from our team migrated all our content across via API, and we had the benefit of already hosting our images directly inside Wasabi instead of Zendesk, which cut out a little complexity.

 

## Building the Knowledge Base

There are knowledge base plugins out there, some of which even look pretty cool, but it seems both unnecessary and like a good way to trap yourself in a box. We went with a custom post type.

A custom post type (CPT) is a simple, sensible, and easy solution. Other use cases may not even need a CPT and could just use posts. It all depends on how you’re building it.

To build a good knowledge base you need at least 2 things, but also likely a third as well. These are: –

Below are the tools we used and why we used them.

### Search Plugin

This was our most important consideration.

We needed a really good search solution to make the whole project worthwhile. I had originally planned to use Elasticsearch (and had some grand plans for it) but it was overkill for what we needed. Tobi recommended JetSearch which is what we ultimately settled on and it has been great. It’s super quick and accurate, and it’s very easy to customize.

It requires Elementor though, so it’s not an option for everyone.

One of our clients also built an awesome knowledge base and they’re using Algolia for their search solution. It looks interesting, and it’s definitely worth a look if you’re building something similar.

### Custom Post Type (CPT)

There are plenty of great CPT solutions around (like the popular Custom Post Type UI), and creating one via a custom plugin is simple enough as well. As we were already using JetSearch, we used JetEngine from the same company. It offers a huge amount of functionality and this one isn’t reliant on Elementor. It’s likely we’ll never make full use of its potential though, so at some point, I may end up replacing it with a simple custom plugin instead.

Side note: This is plugin territory, not theme territory. There’s no benefit to creating your CPT via your theme instead of a plugin.

### Global Blocks

Being able to create a reusable block of content that could easily be inserted into multiple pages was a must. This was incredibly important for us moving forward.

We needed to be able to create a few different types of content and push changes to them across all pages without having to edit those pages individually. Our documentation is simply too large to make major updates one article at a time, and this allows us to manage it much more effectively.

If you’re here because you’re building your own knowledge base, this is an important consideration to keep in mind.

An example of one of these blocks is a list that links to all our “connecting to your server” articles. It appears on almost every article that requires you to SSH into your server.

If we need to update that list in the future, we can do it easily by editing it on any page where it appears, and those changes will immediately go live on all other pages that use it. We’ve actually already done this once already.

We use Elementor’s Global Widgets feature for this. Elementor has pros and cons, but it made building our knowledge base a breeze.

### Wasabi for Image Hosting

We used Wasabi to host our images while at Zendesk and we continued to do so after we moved. Keeping them offsite keeps our main website lean (our media library isn’t a huge mess and we don’t have numerous versions of the same images that we’ll never use) and it also makes managing them a little easier.

Inside Wasabi each individual article that has its own images has its own corresponding folder.

 

## The Design and the Future

Plans for our knowledge base in the future include more videos and learning paths that will make it easier to get started on the platform and do a deep dive into different topics.

As we’ve built it on WordPress this will be extremely easy to implement and you will see new additions here and there as time goes on.

### Knowledge Base Overview Page

The knowledge base page is entirely custom. We can pick and choose what we consider to be the most useful and/or widely used articles to show right up front, and swap them out manually as needed. The entire page can be configured just like any other page, and this was done by taking advantage of Elementor’s built-in page template options.

We implemented the Recently Published section almost immediately after setting it live based on user feedback.

This page conveys a lot of useful information in a way that is easy to scan, making many of the most useful articles available in one click.

### Category Pages

The category overview pages were originally similar to Zendesk by design, but in June (2022) I overhauled all of them. Since our original move, it has grown by over 150 articles, and both the categorization of articles and all of these individual overview pages needed some love to make it easier to browse different topics more efficiently.

Each of those pages is also custom-built and we can modify them individually, just like we’ve done with the Getting Started page and SSL Certificates page.

This way we can highlight a few issues that frequently come up with new users such as the Cloudflare “too many redirects error”. As we continue developing new documentation we will endeavor to continue improving our overall knowledge base UX.

### Single-KB Custom Post Type

We wanted our blog and knowledge base to have a different look and feel from one another as their general purpose is different.

The knowledge base is there to solve problems whereas the blog is for GridPane company updates and more broad topics that are applicable to anyone who is interested in WordPress.

The article layout is clean and simple, and the sidebar contains our search bar and links to all the category pages. The ability to search or jump into a specific category is quick and easy. You can’t miss them.

### pre and code Styling

Our pre and code styling is simple and fairly unique. You’re not going to mistake our articles for any other website out there.

Also, since Elementor Pro v3.1, there’s now a code highlight block that is pretty nifty. I’ve added our existing style to the out-of-the-box setting and I’ve used it in several articles.

 

## That’s a Wrap

That about covers it! This is how and why we rebuilt our knowledge base on WordPress. If you’re building your own WordPress knowledge base, we hope this was a helpful read!

 

 

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

 

 