# Clone Over an Existing Site | GridPane

# Clone Over an Existing Site

 

3 min read 

## Introduction

In addition to our cloning and staging features, GridPane allows you to clone any existing website OVER another existing website.

This means you have now more than regular staging pushes at your disposal in your development work flow, and it also means that if you keep a copy of one or more websites on another server (without using Failover), you now no longer have to delete them and then run a clone, you simply clone right over it to bring it up-to-date.

### Settings that Transfer when using Clone Over

During the Clone over the destination site will be switched to the same owner as the source site, and the process will match the following setting:

We will also duplicate your site-specific PHP in settings and PHP process manager settings that GP-CLI manages, alongside the GP-CLI adjusted site-specific Nginx/OLS settings and any includes in your site level Nginx/OLS directory.

The above all said, you should always check the destination site to ensure that everything is configured correctly once the process has completed.

 

 

### Important: Deactivate WP_DEBUG First

If you've had WP_DEBUG active, be sure to deactivate it before you proceed as it may cause a fatal error on the destination site.

## Step 0. SSL Preparation (if applicable)

An SSL attempt will be made for the destination site IF SSL is enabled on the original site. For this reason, it is important to make sure that your DNS is resolving correctly for the destination site before you attempt your clone over. This will speed up the search and replace because the system will just run a single compound regex.

If DNS is not resolving the clone over will proceed as normal and the SSL attempt will fail, and GridPane will ensure that all URLs in the database for the new site are replaced with HTTP variants, and this requires 3 passes instead of 1. You can then manually enable SSL later.

You can learn more about GridPane search and replace functions here:

GridPane Database Rewrites and Workflow

 

## Step 1. Navigate to your Sites page

Click on the Sites link in the GridPane main menu to go to the Sites management page.

 

## Step 2. Open the site customizer

Click on the URL of the site you want to clone a duplicate of in the active site’s panel.

This will open the site customizer.

 

## Step 3. Open the Clone tab

Click through to the Clone tab in the site customizer. Here you will find the Migrate/Clone tools. Here you’ll find the cloning and clone over tools:

 

## Step 4. Run Your Clone Over

Select your server and then the website you wish to clone over, then click the Migrate / Clone Now button:

Confirm your site and server are correct, and choose whether you want to include database rewrites (run a search and replace):

The process will keep you updated with notifications as it progresses, and let you know once it’s complete.

 

## Step 5. Check Your Destination Site

Now your clone over is complete, be sure to check over the destination site is all working as expected, and clear the cache if necessary.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

