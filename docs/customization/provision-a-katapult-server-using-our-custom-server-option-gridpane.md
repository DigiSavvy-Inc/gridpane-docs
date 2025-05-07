# Provision a Katapult Server Using Our Custom Server Option | GridPane

# Provision a Katapult Server Using Our Custom Server Option

 

7 min read 

Custom Server Provider Notice
While we strive to make our platform available on any matching provider via the custom server option, we cannot guarantee that all custom servers will work with our platform. Available support/debug is therefore limited and at our discretion. If your custom server fails to provision successfully, please make sure you go through this guide in its entirety before requesting support: [Troubleshooting: Custom Server Won’t Provision and is Stuck at 10%](https://gridpane.com/kb/troubleshooting-custom-server-wont-provision-and-is-stuck-at-10/). 

## Introduction

In this article, we’re going to provision a Katapult VPS and then install GridPane from the command line. While we don’t have an integration with Katapult, setting up a server with them is a straightforward process.

### Table of Contents

 

 

### Important

GridPane requires a BRAND NEW KVM virtualized VPS or bare metal server with only standard Ubuntu 22.04 LTS (recommended) or 20.04 LTS image installed. 
Once initial provisioning is complete at the provider, log in to your server via console or SSH and run our provisioning command as ROOT.
Please do not use servers with less than 1GB of RAM as these cannot be supported and don't offer adequate resources for both the server stack and your websites.
Please do not use servers that have less than 30GB disk space.
GridPane does not support ARM servers.

## About Katapult

Katapult is a new, up-and-coming IaaS provider based out of the UK, with data centers in London and the USA East and West Coast. Many more data centers are planned, including multiple locations in Europe and Asia – the bottom of their homepage.

We ourselves at GridPane have used Katapult for numerous projects and highly recommend them.

Not only do they offer excellent performance, but they are powered entirely by renewable energy, which very few other providers worldwide can say. Environmental sustainability is at the heart of their offering, and they also actively contribute to restoring and extending natural forest habitats through native tree planting and more.

New accounts are offered $100 / £100 in free credits to get started. Below, we’ll look at how you can spin up a server at Katapult using our Custom server option.

 

## Step 1. Create a Katapult Account

If you haven’t already, head over to katapult.io, create an account, and log in to your dashboard.

 

## Step 2. Create a Server

Inside your Katapult dashboard, click through to Compute in the left-hand menu. Here you’ll see a green button labeled “Add a new virtual machine“. Click this to begin:

### 1. Location

Next, choose your preferred data center location:

### 2. Operating System

Next, you’ll see a list of operating systems. Choose Ubuntu 22.04 (recommended) or Ubuntu 20.04:

### 3. Choose Your Server Type

Now, you can choose the server specs that you want to use. You’ll likely want to go with the “High CPU – Rocks”  option for most projects:

Scroll down to the bottom and click the “Continue” button to confirm your choice:

### 4. Give it a Name

Next, give your server an easy-to-identify name and hostname. You can also add a description and tags if it makes sense to do so:

### 5. Disk Space

Below the naming options, there are 3 additional tabs. The first is disk space, and if you’d like to add additional disk space to the server configuration you’ve chosen, you can do so here:

### 6. Password and Keyboard Layout

The next tab is called Advanced Options, and here you can set the root password (or leave it blank and have Katapult auto-generate it) and choose your keyboard layout.

Neither of these particularly matter, and nor does the SSH Key tab below, as all we need to do is connect to the server and run the GridPane provisioning script, and our scripts will then lock the server down and, if set in your account, add your SSH keys to the server for you.

Now click the “Continue” button at the bottom to create the server.

### Your Server Will Now be Created

Once you click Continue, the server will immediately begin to build:

And it’s pretty speedy!

Click the “Go to my new server →” button to go to your server configuration page.

 

## Step 3. Copy Your Server IP Address

Inside the server’s configuration page, you’ll see your server’s IP address. Click the copy button as we need it for the next step.

We’ll come back to this page shortly.

 

## Step 4. Create Your Server Provisioning Code

Back in your GridPane dashboard, navigate to your Servers page and click on Custom VPS:

### Configure Your Server

Enter the name, server IP address, and the data center name you wish to use.

Note: The data center name is for your reference only, so feel free to give it a name that makes the most sense for you. As this example’s server is in London, we’ll go ahead and enter this.

 

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

 

Once you click Create Server, a popup modal will contain your root password and a command-line string. Copy that string and paste it into a text document – you’ll need it in a moment.

 

## Step 5. Run Your Provisioning Code

Head back to your server configuration page inside your Katapult account.

If you haven’t already, paste the string from the last step into a text document.

### Open Up the Server Console

Now, copy your root password, and then under Actions on the right-hand side, click “Access Console” to open up your server’s console:

### Log in as Root

Log in as the root user using the password you have just copied:

### Paste Your Provisioning Code

Now, inside your server, paste your provisioning code and hit Enter. Our script will then begin to run and provision your server.

The script will run for a few minutes and then end with the following:

At this point, you can close the console, and the rest of the process will take around 10 minutes. You can track this inside your GridPane account.

 

## Step 6. Wait for Approx 10 Minutes

You can monitor the rest of your server’s provisioning progress inside the Servers page of your account. Approximately 10 minutes later, it will be ready to use inside your GridPane account.

 

## Congratulations! Next Steps

Now that your server is live, you’re ready to start creating and configuring new WordPress websites.

To deploy a site, click on the Sites link in the GridPane main menu to begin the process. We have a separate article that details the steps in detail for you.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

