# Provision a DigitalOcean Droplet using the DigitalOcean API | GridPane

# Provision a DigitalOcean Droplet using the DigitalOcean API

 

5 min read 

## Introduction

In this article, we are going to provision a DigitalOcean Droplet directly from within our GridPane dashboard using the DigitalOcean API. This article will be using the Digital Ocean nomenclature Droplet and the word Server interchangeably.

### Table of Contents

 

 

### Information

When you first create your DigitalOcean account, they may not allow you to choose servers with dedicated vCPU's while on free trial credit. This can usually be resolved quickly by reaching out to their support. This doesn't affect most of the servers that the GridPane community usually use.

## Step 1. Create a DigitalOcean Account and Login

If you don’t already have a DigitalOcean account, you can get yourself $100 free credit when you first get started. Full disclosure, this is our affiliate link:

https://try.digitalocean.com/performance/?refcode=3e9e7a6f9f97

You’ll need to verify your email address to complete your sign up. Once complete, login to your account. 

## Step 2. Generate a New API Token

Inside your DigitalOcean Account click on API in the top menu bar:

In the Applications & API panel that opens up, click on the Generate New Token Button in the Tokens/Keys tab.

 

### Generate a Token with the correct scope

In the New personal access token popup modal, give your access token an appropriate name, such as GridPane. Then make sure both Read and Write are selected in the scope, before clicking Generate Token.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1594'%20height='1064'%20viewBox='0%200%201594%201064'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Provision-Digital-Ocean-Droplet-using-the-Digital-Ocean-API/5d77bf1d6f3ec.png) 

## Step 3. Copy Your Personal Access Token

DigitalOcean will now display your Personal Access Token. It will not be shown again for security purposes, so make sure you remember to copy it to enter in to your GridPane settings in the next step. Remember to keep this access token safe and secure.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2190'%20height='920'%20viewBox='0%200%202190%20920'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Provision-Digital-Ocean-Droplet-using-the-Digital-Ocean-API/5d77bf1e76914.png) 

## Step 4. Add Your Token to GridPane

Login to your GridPane account and click the Your Settings link in the dropdown menu accessible by clicking on your username and icon.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/click-to-settings/Click%20to%20settings.png) 

### Enter your DigitalOcean Personal Access Token in GridPane

Locate and click the Integrations option in the left horizontal menu, and then within Cloud Providers select DigitalOcean, and then enter your Personal Access Token you copied in Step.4 above into the Token input field, give your key a name, and then click Create.

 

### View/Edit your DigitalOcean API Token

Your Digital Ocean API Token will now be available from this settings panel. If you wish to edit or change your API Token you may do this by clicking the down arrow for your specific key, and then clicking the edit button with the blue pencil icon.

 

## Step 5. Provision Your First Droplet

Now that you’ve added your DigitalOcean Personal Access Token to GridPane you are able to provision Instances with it from within GridPane. First, navigate to the Servers page in your account:

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='0'%20height='0'%20viewBox='0%200%200%200'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Provision-Vultr-Instance-using-the-Vultr-API/servers-page.png) 

 

### Information

For servers that are 8 vCPU's or less, we typically recommend DigitalOcean's Premium AMD Droplets for best performance.

Select DigitalOcean from the choice of Cloud VPS providers and a configuration panel will open.

Enter an appropriate name for your Droplet, and then choose a server plan and region from the dropdown selectors, before choosing whether or not you wish for DigitalOcean Backups to be enabled.

 

### OS Version

We recommend that you choose Ubuntu 22.04 LTS as the default OS.

### Choose Your Web Server

You have the option to choose between Nginx and OpenLiteSpeed. This is largely personal preference. If you’re unsure which one to choose, start with Nginx.

### Choose your database

If you’re on the developer plan you’ll have the option to choose between Percona and MariaDB for your database.

Percona is a drop-in replacement for MySQL and includes security, availability, and availability features that are only available in enterprise MySQL. It has removed query caching, and it has more advanced aspects for things like storing and managing JSON as a storage format.

MariaDB could mean fewer issues importing old WordPress websites from low-quality hosting environments. It will likely use less RAM than Percona and may offer performance benefits for some websites.

Both are excellent options.

### Provider backups

We highly recommend that you enable provider backups. It’s a small price to pay for the extra insurance they offer.

Additional note: You will need to set this up directly at your server provider when using our custom server option.

### Create your server

Click the Create Server button when you are happy with your configuration choices.

 

## Step 6. Wait for 10-15 Minutes

GridPane will begin provisioning your server. You will now be able to see your server in the Active Servers list.

At any time during the provisioning process, you may check what stage the process is at by rolling over the progress bar, a popup window will display the current job being completed.

Once GridPane has finished provisioning your Instance the progress bar will turn green and you will be able to deploy some Serious WordPress Sites on it.

Of course, you can create multiple servers at the same time by clicking on a Cloud provider and repeating the above steps at any time during the provisioning process.

 

## Congratulations! Next Steps

While not always necessary, you may need to whitelist our IP addresses within your DigitalOcean account. This is quick and easy, and you can learn about why and how to do this here:

Whitelisting GridPane at Your Server Providers

### Create WordPress Sites

Now that your server is live, you’re ready to start creating and configuring new WordPress websites.

To deploy a site click on the Sites link in the GridPane main menu to begin the process. We have a separate article that details the steps in detail for you.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

