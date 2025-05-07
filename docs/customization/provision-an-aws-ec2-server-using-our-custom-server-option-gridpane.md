# Provision an AWS EC2 Server Using Our Custom Server Option | GridPane

# Provision an AWS EC2 Server Using Our Custom Server Option

 

9 min read 

Custom Server Provider Notice
While we strive to make our platform available on any matching provider via the custom server option, we cannot guarantee that all custom servers will work with our platform. Available support/debug is therefore limited and at our discretion. If your custom server fails to provision successfully, please make sure you go through this guide in its entirety before requesting support: [Troubleshooting: Custom Server Won’t Provision and is Stuck at 10%](https://gridpane.com/kb/troubleshooting-custom-server-wont-provision-and-is-stuck-at-10/). 

## Introduction

In this article, we’re going to provision an Amazon EC2 VPS and then install GridPane from the command line. Throughout this tutorial, we’ll use “VPS” and “Instance” interchangeably. This article assumes that you don’t require more than the basic setup options for your VPS and is designed to get a server up and running quickly.

### Table of Contents

 

 

### Important

GridPane requires a BRAND NEW KVM virtualized VPS or bare metal server with only standard Ubuntu 22.04 LTS (recommended) or 20.04 LTS image installed. 
Once initial provisioning is complete at the provider, log in to your server via console or SSH and run our provisioning command as ROOT.
Please do not use servers with less than 1GB of RAM as these cannot be supported and don't offer adequate resources for both the server stack and your websites.
Please do not use servers that have less than 30GB disk space.
GridPane does not support ARM servers.

## Step 1. Configure and Launch an EC2 Instance

Login to your AWS Management Console and click through to EC2. EC2 can be located in the “Compute” service list as shown below, or you can search for “EC2” in the Find services search.

EC2 is making changes to its UI. At the time of writing, this is what it looks like:

Be sure to check you’re launching in the correct region in the top right-hand corner. I’ll be selecting London for this instance:

Next, you can either click through to instances or click the orange Launch instance button:

### Choose an Amazon Machine Image (AMI)

Here, use the search bar to bring up the Ubuntu images. Locate Ubuntu Server 22.04 LTS (HVM) or 20.04 LTS (HVM), SSD Volume Type”:

Please note that ARM servers are not supported by GridPane, and they will not be able to provision successfully.

### Choose an Instance Type

EC2 has A LOT of options to choose from. I’m keeping it simple with a t3.medium instance – 2vCPU 4GB RAM. The t2.small would be the smallest we recommend – we don’t recommend you use any VPS with less than 2GB RAM.

You can see the instance specs as highlighted below:

### Configure Instance Details

This part is a little more complex. We’ll be keeping most of it as the default setting, but adding in a couple of optional extras. Here are the options I’m selecting:

### Add Storage

I’ve chosen 80GB General purpose SSD – you may select whatever size best suits your needs. General-purpose SSD is suitable for most purposes, but you can learn about the available storage options here:https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volume-types.html

Update: One of our awesome clients sent this in: “AWS recently launched GP3, which has a much higher base IOPS than GP2, does not suffer from a credit bucket system and throttling while being roughly 20-25% cheaper than GP2 and without the risks of unexpected costs”.

GP3 storage is the better option to go for when choosing between GP2 and GP3.https://aws.amazon.com/about-aws/whats-new/2020/12/introducing-new-amazon-ebs-general-purpose-volumes-gp3/

### Add Tags

Here, I’ve given my VPS a name, and I’d recommend you do the same, as it will make it easier to manage your servers at a glance.

### Configure Security Group

Here, we need to set up our firewall rules. We need to set SSH, HTTP, and HTTPS (which will all default to the correct value) and then a custom rule.

For the custom rule, select “Custom TCP Rule” and set the port to 11371, and select “anywhere” under source.

This custom Firewall rule will allow all incoming traffic from any IP address to your server’s TCP port 11371.

GridPane’s security will lockdown and protect this port from any traffic originating from any location other than GridPane directly on the instance via UFW.

Note: I haven’t done so in the image above, but here, you can give your security group a specific name like “GridPane Servers” and reuse it on any future servers that you spin up.

### Review and Launch

Review your details and click Launch in the bottom right-hand corner.

You’ll be asked to select an existing key pair or create a new one. Feel free to select a pre-existing pair if one already exists, but if not, you’ll need to create a new one. You’ll need this to connect to your server in step 5.

Next, click the Launch Instances button, and in a few minutes, your new server will be live.

 

## Step 2. Setup a Static IP

Now that we’ve created our instance, we need to give it a Static IP. This is VERY IMPORTANT as GridPane cannot manage your server without having a Static IP Address to reference, and the other options AWS provides during the setup of your EC2 instance may not persist forever.

Select “Elastic IP” from the left-hand sidebar:

And then click the orange “Allocate Elastic IP Address” button:

Click the allocate button:

We now have a static IP address that we can associate with our server. Select “Associate static IP address” from the actions dropdown (or click directly on the IP address):

Then, choose your instance and click the “Associate” button.

You’ve now associated your IP with your EC2 instance! Phew… nearly there.

 

## Step 3. Connect Your Server to GridPane

Back in your GridPane dashboard, click on Custom VPS from the servers page.

### Configure Your Server

Enter the name, IP (the elastic IP Address we set in Step 3), and the data center name you wish to use.

Note: The Datacenter name is for your reference only, so feel free to give it a name that makes the most sense for you. As this example server is in London, UK, we’ll go ahead and enter this.

 

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

 

Once you click Create Server, a popup modal will contain your root password and a command line string. Copy that string – you’ll need it in a moment.

 

## Step 4. Connect to Your EC2 Server

Connecting to your EC2 instance isn’t as simple as connecting to a Lightsail instance. Please see Amazon’s documentation on how to connect:

https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/AccessingInstances.html

NOTE: You may need to first protect your key.pem with the following command:

```
chmod 400 /path/to/key.pem
```

### Connecting

In my case, I’m using Cmder. First, I add:

```
ssh -i
```

Then drag and drop the key file I created into Cmder to add in the correct key path, and then finish by adding the highlighted server path:

In full-on Windows it looked like this in my case:

```
ssh -i "C:\Users\Username\Desktop\GridPaneEC2London.pem" [ubuntu@ec2-18-132-121](https://gridpane.com/cdn-cgi/l/email-protection#2c594e594258596c494f1e011d14011d1f1e011d1e1d)-28.eu-west-2.compute.amazonaws.com
```

 

## Step 5. Run Your Provisioning Command

Now inside your server, we need to run our provisioning code as the root user. To switch to root, type:

```
sudo -s
```

We’re now ready to enter the string copied from the GridPane Custom VPS popup modal to install GridPane:

This will initiate Stage 1 of installation.

A few minutes later, you’ll see this:

And you can now monitor your VPS’s progress inside your GridPane account.

### Wait for 10-15 Minutes

In around 10 minutes or so, your server will be ready to go:

 

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

