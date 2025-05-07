# Easily Deploy a GridPane WordPress Site | GridPane

# Easily Deploy a GridPane WordPress Site

 

10 min read 

## Introduction

GridPane simplifies the process of deploying WordPress sites in a much more secure manner than the traditional WordPress 5 Minute Installation.

The GridPane automated WordPress deployment creates your database and installs a fully functioning WordPress site with admin user and password all from within the protected environment of your GridPane dashboard.

### Table of contents

GridPane will deploy your site’s WordPress core to the absolute path on your server of:

```
/var/www/{site.url}/htdocs
```

 

## Step 0. Configure DNS Records (Optional)

To view your website, you can use a local hosts redirect, or set your DNS records for your domain. To learn more about using a local hosts redirect, please check out the following step by step guide:

How can I edit my local hosts file to redirect URLs

If you’re not using a local host redirect, you must configure DNS records for your domain at your domain registrar and DNS provider before you can visit your WordPress site.

Since it can take some time (from several hours up to 48 hours) for your DNS changes to fully propagate, it is advised that you configure your DNS records prior to deploying your WordPress site.

### GridPane DNS API Integrations

GridPane features integration with the DNS Made Easy API and Cloudflare API.

If you are a DNS Made Easy Customer you can enable DNSME DNS configuration as you deploy your site.

If you’re using Cloudflare you can enable Cloudflare DNS configuration as you deploy your site.

If you’re new to DNS management, you can learn more about the fundamentals in these two guides:

 

## Step 1.  Navigate to the Sites page of your account

Click on the sites link in the GridPane main menu to begin the process of deploying a Serious WordPress site.

 

## Step 2. Configure your WordPress site

At the top of the Sites page you will see the Add New Site panel.

More stack specific options (Nginx/OpenLiteSpeed) will be shown once you select your server.

The following input fields will need to be completed:

 

### 1. URL

First add your domain name in the URL input field.

Do not enter your site URL with the www host prefix. All GridPane sites are created with the correct Nginx configuration to serve both www.yoursite.com and yoursite.com.

 

### 2. Server

Choose the server you wish to deploy to from the Server dropdown selector.

We have easy to follow tutorials which provide step by step guides to provisioning server instance from several different infrastructure providers here.

 

### 3. Create / Assign a System User

You have the ability to create a new system user or assign your site to an existing user.

For security reasons, we highly recommend that you put each website on their own individual system user to keep them isolated from one another at the server level.

A major security issue with most shared hosting is that all the sites in the account typically use the same system user. This means that if one site is ever compromised, it can potentially compromise every other site in the account.

At GridPane you can auto-create a new user, create a new user with a custom name, or assign the site to an existing user.

Autocreate:

Custom:

It’s important to keep your sites isolated for fundamental security, and so you can accurately monitor system resources per website on the command line if you need to.

It’s also useful if you want to give different users SSH/SFTP access to different sites on the server.

 

### 4. Set Your WP Users

Here you can set up WordPress users for your website.

When creating new websites you have 3 options: –

Inside your Settings page, you can set your Default WP Admin Username, Email, and Password settings. Learn more here:

Using Default WordPress Admin Settings to deploy GridPane sites

 

### 5. Choose a GridPane Bundle to deploy (Optional)

If you wish you may select a GridPane Bundles to use to deploy a site preconfigured with your most commonly used themes and plugins.

We have an easy to follow step-by-step guide to using GridPane Bundles here.

You may also be interested in creating a blueprint website for your account.

 

### 6. PHP Version

Choose your preferred PHP version. You should always use the supported PHP versions:

Occasionally, we see some strange behavior with plugins that are NOT ready for the most recent PHP version. Sometimes you’ll immediately see a critical error.

In these cases you can fix the issue by using an earlier version, however, you should then push to staging or make a clone of the website and update your codebase to ensure it’s compatible with a current supported version of PHP.

 

### 7. PHP Worker Settings

If you’re not sure which setting to choose, we highly recommend you stick with our default settings. These will serve you well for 95% of websites, and still pretty well for the other 5%.

You can learn more PHP workers and our recommended settings for different types of websites in this blog post:

PHP Workers and WordPress: A Guide for Better Performance

If unsure, stick with the default Dynamic / ProcessGroup settings.

##### Nginx:

##### OpenLiteSpeed:

 

### 8. Caching

In the beginning, you may want to leave caching turned off until you have imported your site in, or finished your development work.

If not, here you can choose your preferred setting. You can also learn more about caching strategy in this article:

What is the optimal caching strategy for GridPane, should I run a plugin cache?

##### Nginx:

##### OpenLiteSpeed:

##### Our recommendations in a nutshell:

 

### 9. WAF

We recommend you set up your WAF right from the get-go.

If you have a Pro account, you have the 6G WAF available.

If you have a Developer account, you have the 7G WAF and ModSecurity (ModSec) available.

For most websites, we recommend the 7G WAF. ModSec is a great selling point for Enterprise level clients, but it’s also more resource hungry and more difficult to fine-tune. 7G is super lightweight and customizable and great for most websites.

 

### 10. SMTP

GridPane does not come preconfigured with email functionality (which is highly unreliable when not using a reliable service with proper DNS records), but we do have a direct integration with SendGrid and more integrations are on the way.

Using SendGrid SMTP for Transactional Emails

 

### 11. SSL Certificate

If you are using one of our DNS API integrations below, or have your DNS records already set up and pointing to your server, you can automatically provision an SSL certifcate.

For this, select the Primary Domain SSL option.

NOTE: AutoSSL is only necessary for WordPress multisites/WaaS networks where you want to automatically provision new SSL certificates for new addon domains.

 

### 12. DNS API Integration (If Applicable)

If you have added a DNS Made Easy API key or Cloudflare API key in your system settings, you have the option to launch your site with your integration set. If it’s a brand new site it will with no records this will automatically update your DNS. You can select your chosen provider from the dropdown.

We highly recommend Cloudflare, and you can manage all of your websites for free using their free plan. Here’s our documentation:

Using Cloudflare with GridPane

 

### 13. Local Backups (Recommended)

Local backups (backups taken directly on your server) can be set hourly, daily, weekly, or monthly. These can be used for quick recovery if a client makes a breaking change or a team member accidently deletes the wrong site etc. Both local and remote backups are incremental, and we highly recommend them.

Here you can set the frequency, the exact time they take place (you may want to add a little time between each backup), the retention schedule, and when to pause them if your disk space runs low.

Our local backup documentation can be found here:

V2 Backups Part 2. Setting Up Local Website Backups

 

### 14. Remote Backups (Optional)

Like local backups, we also highly recommend setting up remote backups so that should your server ever go offline for any reason you can recover your sites on a different server.

Here you can set your backup and retention schedules, and choose the provider (AWS S3, Backblaze B2, or Wasabi):

Our full remote backup documentation can be found here:

V2 Backups Part 3. Setting Up Remote Website Backups

 

### 15. Git Integration (Optional)

If you’ve set up a Git repository in your account that you would like to use for your new site, you can set up the integration by selecting the repository and then the branch:

We will then automatically deploy your site using your repo.

Our full documentation for getting started with the GridPane Git integration can be found here:

Git Integration Documentation

 

### 16. Configure Advanced Options (Optional)

The Advanced Options section has several preselected checkboxes that will configure a Staging Site and the GridPane Automatic Updates feature.

GridPane Staging Sites allow you to push from your live production site to your staging site, or from your staging site to your live production site, at any time. Learn more about Staging here:

Using staging sites on GridPane

The Automatic Updates use GridPane UpdateSafely™ to utilize an automated visual comparison when updating your site’s plugins and themes to ensure site integrity is maintained. Learn more about UpdateSafely™ here:

UpdateSafely™ 2.0

 

### 17. Deploy your WordPress Website

Once you have entered the appropriate configuration parameters to suit your needs click Add site to being deploying your Serious WordPress site on GridPane.

 

## Step 3. Wait a few moments while GridPane deploys your WordPress Site

GridPane will immediately begin deploying your Serious WordPress site. You will receive a green success notice banner and your site will now be displayed in the Active Sites list below the Add New Site panel.

While the deployment process is still ongoing you will see spinner icons for each of the aspects of the deployments progress.

Behind the scenes GridPane is creating a database, installing WordPress with an Admin User, creating a staging site and configuring automatic updates and UpdateSafely™, installing the Nginx helper function, and configuring Nginx FastCGI caching and Redis Object caching for your site and more.

This is not your average WordPress site deployment! Please be patient while GridPane is working its magic (it’s pretty quick).

Once the deployment is complete the spinner progress notifications will be replaced by green ticked checkboxes and the DB icon will turn green.

 

## Step 4. Login to your WordPress site and do great things!

Your WordPress site is now ready for you to create your project.

Visit your site by going visiting the admin URL at either

http://your-site-domain.com/wp-admin

or

https://your-site-domain.com/wp-admin<p”>Depending on whether you have enabled an SSL or not. You will be redirected to the WordPress login page.

You will need to enter either your Admin Username or Email Address and Password.

If you have set your Default WordPress Admin Settings,  then you will use these credentials to login in.

If you are not using a Default WordPress Admin User, then GridPane will have set your Username and Email address using your GridPane account user, and will have generated a strong password.

You can find these Admin User login details in your site log. Click on the log icon to open it up:

Enter your WP Admin User credentials and click log in.

You’re now all set to get started building your WordPress website!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

