# Adding Multiple API Keys to Your GridPane Account (Multi API) | GridPane

# Adding Multiple API Keys to Your GridPane Account (Multi API)

 

6 min read 

## Introduction

GridPane now includes the ability to add multiple API keys for different providers within Developer and Agency accounts.

This means that instead of being restricted to one key per provider, you can now, for example, have your own DigitalOcean API key active, and a clients DigitalOcean API key active at the same time, and use both to create servers in each account.

### Developer Plan

The Developer plan includes the sum total of the number of API integrations for your number of API keys. At the time of writing, this is a total of 12 keys, one for each provider.

You can distribute these keys between the available providers as makes sense for you. For example, if you don’t use Lightsail or DNSME, and don’t have API keys active for them inside your account, you can use these 2 additional free keys slots for other providers, such as adding an extra Cloudflare account and an extra DigitalOcean account.

### Agency Plan

Agency includes a total of 50 available API keys.

 

## Add Your API Keys

You can add your API keys inside your Settings page within your account.

### Step 1. Navigate to the Settings Page

Click on your name in the top right-hand corner and select Settings from the dropdown.

Inside your Settings, you will see Integrations in the left-hand sidebar menu. Click through and here you will find the available API integrations as well as how many API keys you have left remaining (highlighted in red).

### Step 2. Add Your API Keys

Inside Integrations is where you can add all of your API keys to your GridPane account, and this of course includes adding more than 1 key to different providers.

For example, in the image below I have 2 DigitalOcean accounts set up, which means I can now create servers from two completely separate DigitalOcean accounts.

 

 

### Info

All existing API keys in your account before we rolled out the Multi API update had no name assigned to them. To ensure you are able to easily distinguish between different keys, we've added this functionality into the dashboard. For API keys that existed before the update was rolled out, we have automatically assigned a name to them based on a Star Wars name generator (because we're cool). Please feel free to rename them as you see fit.

## Multiple Server API Keys

In the above example, I’ve added 2 DigitalOcean API keys. Now, when I head over to my Servers page, I can select the specific DigitalOcean server I want to use from the API Key dropdown:

The same is true for each provider. Once you’ve added more than one API key, you will be able to select the specific account that you want to use to create your new server. Make sure you name your keys appropriately so that you can easily distinguish between them.

You can learn about getting started with your preferred server providers and creating your API keys in this section of the knowledge base:

Provisioning Servers

 

## Multiple DNS API Keys

When adding multiple DNS API keys for Cloudflare or DNS Made Easy, you can select the specific account you want to use when creating your websites or in the website customizer.

When creating your websites, wou first need to select Cloudflare or DNSME, and then a dropdown will appear where you can select the API key:

You can then change or add a key anytime by clicking on your website to open up the website customizer, clicking through to the domains tab, and click under API Integration:

This will open the model where you can change the DNS API integration settings. First, choose the DNS API integration you want to use, and then select your key:

You can learn more about setting up Cloudflare and/or DNS Made Easy with GridPane in the following articles:

Using Cloudflare with GridPane

Using DNS Made Easy (DNSME) with GridPane

 

## Multiple Backup Provider API Keys

Our V2 backups system allows you to connect your servers to 4 different external storage providers (external backups are not available on V1):

Once you’ve set up your backups API key/s, head over to your Sites page and click on a website to open up your website’s customizer. Here in the backups tab is where you can configure your backup settings:

When restoring a site, you’ll also be able to choose the specific API key as well.

For a full rundown on V2 external backups, and each of the providers we connect to, please see the following articles:

 

## Multiple SMTP API Keys

When adding multiple SMTP API keys, you can select the specific account you want to use when creating your websites, and also inside the site customizer.

When creating your websites, your API keys will appear in the SMTP Integration dropdown menu:

You can then change this anytime by clicking on your website to open up the website customizer and selecting your preferred key from the dropdown:

The toggle will be inactive until a key is selected.

You can learn more about setting up SendGrid with GridPane in the following article:

Using SendGrid SMTP for Transactional Emails

 

## Downgrading Your Account

If you’re planning to move to a lower-tier plan, e.g. Agency > Developer or Developer > Pro, you’ll need to ensure that your API keys are within the allowed limit detailed in the introduction. If going to Pro, you’ll also need to ensure that multiple API keys are not being used for any providers.

Once that’s taken care of, the application will allow you to proceed and downgrade.

 

## Multi API and Team Members

GridPane offers 3 different types of teams members that you can use to give additional people access to your account. Full details of how to use our teams feature can be found here:

Using GridPane Teams

Below details the Multi API permissions for each type of team member.

### Admins

### Staff

### Clients

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

