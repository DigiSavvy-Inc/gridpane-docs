# Provision a Vultr Server Using the Vultr API | GridPane

# Provision a Vultr Server Using the Vultr API

 

6 min read 

## Introduction

In this article, we are going to provision a Vultr Instance directly from within our GridPane dashboard using the Vultr API. This article will be using the Vultr nomenclature Instance and the word Server interchangeably.

### Table of Contents

 

 

### Information

Vultr API requests are limited to 2/sec. Due to the fact that GridPane allows you to provision servers so quickly, you may face occasional errors if you exceed this rate limit. Our developers are currently working to ensure this rate limit does not adversely affect your server build experience. But, please bear this in mind when provisioning your Vultr servers with GridPane.

## Step 1. Create a Vultr Account and Login

If you don’t already have a Vultr account, you can get yourself $100 free credit when you first get started – simply give it a quick Google search, and it’s easy to find. Note that their free trial credit offers vary in both credit amount and how long they’re valid for.

You’ll need to verify your email address to complete your sign-up. Once complete, log in to your account.

 

## Step 2. Enable the Vultr API

Login to your Vultr Account and click on your name in the top right corner. This will display a dropdown menu and here you can select ”API”:

In the Personal Access Token panel, you will need to enable the API by clicking the large blue Enable API button:

 

## Step 3. Whitelist GridPane IP Addresses

Once the Vultr API has been enabled, locate the Access Control Area (Account → API) to whitelist the GridPane server IP addresses. This will allow the GridPane servers to connect to your Vultr account.

GridPane has three IP addresses that need to be whitelisted:

You can whitelist only these IP addresses by adding them individually if you like:

Alternatively, you can whitelist all IP addresses.

Whitelisting all IP addresses is less secure, if you choose this option, then please ensure you take adequate precautions and keep your API Personal Access Token safe.

If you wish to remove any whitelisted IP address at a later date, just click the large Remove button next to the IP addresses/range you wish to remove.

 

## Step 4. Copy Your Personal Access Token

Your Personal Access Token is available at any time from the API page in your Vultr account area. Copy your token to enter into your GridPane settings in the next step. Remember to keep your token safe and secure.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1321'%20height='632'%20viewBox='0%200%201321%20632'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Provision-Vultr-Instance-using-the-Vultr-API/5d77bf0d5961e.png) 

## Step 5. Add Your Vultr Personal Access Token to GridPane

Login to your GridPane account and click the Your Settings menu item in the dropdown menu accessible by clicking on your username and icon.

Locate and click the Integrations option in the left horizontal menu, and then within Cloud Providers select Vultr, and then enter your Personal Access Token you copied in Step.4 above into the Token input field, give your key a name, and then click Create.

### View/Edit Your Vultr API Token

Your Vultr API Token will now be available from this settings panel. If you wish to edit or change your API Token, you may do this by clicking the down arrow followed by the edit button with the blue pencil icon.

A popup modal will appear, and you can easily change your Vultr Token and click Update.

 

## Step 6. Create a Vultr Server

Now that you’ve added your Vultr Personal Access Token to GridPane you are able to provision Instances with it from within GridPane. First, navigate to the Servers page in your account:

Select Vultr from the choice of Cloud VPS providers and a configuration panel will open:

### Configure Your Server

Enter an appropriate name for your Instance, and then choose a server plan and region from the dropdown selectors, before choosing whether or not you wish for Vultr Backups to be enabled.

 

 

### Choosing a Server

Both Vultr High Frequency and Vultr High-Performance AMD options provide excellent performance and we like and recommend both.

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

 

## 6.1. Troubleshooting: If Your Server Fails to Provision

If your server fails to provision, then it was likely just a blip at either Vultr or one of our repositories. These are very rare and the best next step is to delete the server and try again.

Below are further details to check for.

 

 

### Invalid API Warnings

If you get an error message stating that your API key is invalid, it's like that we're getting a 401 response due to our IP address being "unauthorized".
Here you will need to whitelist our IP addresses, and then you should be all set to try again. This article has all of the details you need:Whitelisting GridPane at DigitalOcean and Vultr

### Errors and Server Availability

Vultr High Frequency servers are in very high demand and frequently sell out. If their API is up-to-date with the current server stock, then those specific servers will not be available to select within your GridPane account when you go to provision a server.

If you see an error such as this:

This means that this server is unavailable, but their API is still sending it to us.

If you’re unsure or want to double-check, if you head to over the server options directly inside your Vultr account, it will show you the current options available as you choose your datacentre and server type.

### Server Stock

Vultr are adding more servers all the time, and it’s likely that your preferred size/datacentre will become available again in the near future, but they sell out fast, so you may want to check frequently.

 

## Step 7. Wait 10-15 Minutes

GridPane will begin provisioning your instance. You will now be able to see your instance in the Active Servers list.

At any time during the provisioning process you may check what stage the process is at by rolling over the progress bar, a pop up window will display the current job being completed.

Once GridPane has finished provisioning your Instance the progress bar will turn green and you will be able to deploy some Serious WordPress Sites on it.

Of course, you can create multiple servers at the same time by clicking on a Cloud provider and repeating the above steps at any time during the provisioning process.

 

## Congratulations! Next Steps

Now that your server is live, you’re ready to start creating and configuring new WordPress websites.

To deploy a site click on the Sites link in the GridPane main menu to begin the process. We have a separate article that details the steps in detail for you.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

