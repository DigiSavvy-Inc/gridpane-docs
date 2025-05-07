# Provision a Microsoft Azure Server Using Our Custom Server Option | GridPane

# Provision a Microsoft Azure Server Using Our Custom Server Option

 

8 min read 

Custom Server Provider Notice
While we strive to make our platform available on any matching provider via the custom server option, we cannot guarantee that all custom servers will work with our platform. Available support/debug is therefore limited and at our discretion. If your custom server fails to provision successfully, please make sure you go through this guide in its entirety before requesting support: [Troubleshooting: Custom Server Won’t Provision and is Stuck at 10%](https://gridpane.com/kb/troubleshooting-custom-server-wont-provision-and-is-stuck-at-10/). 

## Introduction

Azure is not typically a service that we would recommend for hosting WordPress, but there are circumstances where it may be the only provider that you’re able to use for a specific project, or you may have Azure credits you would like to make use of.

If that’s the case, then this guide will walk you through the process of creating and configuring an Azure VM and connecting it to GridPane.

### Table of Contents

 

## Before We Begin

Azure is a platform that people have had problems provisioning new servers with, and it’s usually the exact same problems that happen when provisioning a custom server at a provider that has a complex set of configuration options. In order for your Azure server to work correctly, we’ll need to make sure the following is set correctly.

### 1. Ports

Make sure ports 22, 80, and 443 are open.

### 2. ARM is not Support

ARM servers are not supported by GridPane, and these typically require application versions to be compiled for it in most cases. Most providers don’t offer this as an option, but Azure does (though it’s not selected by default at the time of writing).

 

## Step 1. Configure and Create Your Azure Server

To get started, log in to your Microsoft Azure account, hover over Virtual machines, and create a new “Azure Virtual Machine”.

The following are only guidelines, and you are welcome to explore additional features that Azure offers. We specifically require that you have the correct ports open and do not select ARM architecture, but it’s possible that some other features/configurations may not work with GridPane.

 

### 1. Basics

###### Project details:

###### Instance details:

###### Administrator account:

##### Inbound port rules:

Click the Next : Disks > button to continue.

 

### 2. Disks

###### Disk options:

Leave the default settings.

###### Data disks for “server name”:

Click the Create and attach a new disk option.

Here, you can choose the amount of disk space you want to use and whether you want to delete this disk space when you delete the VM itself. Leave the other options as their default settings.

As an additional note, the “Enable Ultra Disk compatibility” may be worth exploring, but I have not had time to look into it while writing this article.

Click the Next : Networking > button to continue.

 

### 3. Networking

Leave the default networking settings as they are.

Click Next : Management > to continue.

 

### 4. Management

Here, you can leave most of the default settings as they are. However, I would highly recommend that you select one of the two backup options for your server:

Click Next : Monitoring > to continue.

 

### 5. Monitoring > 6. Advanced

Leave the default settings for Monitoring and Advanced and proceed to Tags.

 

### 7. Tags

If you would like to create tags for this server you can do so here.

 

### 8. Review + Create

Here, you can review your settings, and when ready, you can click the Create button to create your new Azure server.

You can also download these settings as a template for future use as well.

The deployment process may take a minute or two to complete, and it will then display a notification once it’s up and running.

You’ll be able to see your resource over on the main Home screen and then again under Virtual Machines.

 

## Step 2. Copy Your Server’s IP Address

To copy your server’s IP address, you will need to open up your server’s configuration settings.

Inside your Azure account, locate your new server on your account home page or inside the Virtual Machines page, and click on the server’s name to open up the settings.

Here, you can copy your IP address:

 

## Step 3. Connect Your Server to GridPane

Back in your GridPane dashboard, navigate to your Servers page and click on Custom VPS:

### Configure Your Server

Enter the name, server IP address, and the data center name you wish to use.

Note: The Datacenter name is for your reference only, so feel free to give it a name that makes the most sense for you. As this example’s server is in Falkenstein, we’ll go ahead and enter this.

 

### Choose Your Web Server

You have the option to choose between Nginx and OpenLiteSpeed. This is largely personal preference. If you’re unsure which one to choose, start with Nginx.

### Choose your database

If you’re on the developer plan, you’ll have the option to choose between Percona and MariaDB for your database.

Percona is a drop-in replacement for MySQL and includes security, availability, and availability features that are only available in enterprise MySQL. It has removed query caching, and it has more advanced aspects for things like storing and managing JSON as a storage format.

MariaDB could mean fewer issues importing old WordPress websites from low-quality hosting environments. It will likely use less RAM than Percona and may offer performance benefits for some websites.

Both are excellent options.

### Create your server

Click the Create Server button when you are happy with your configuration choices.

 

Once you click Create Server, a popup modal will contain your root password and a command-line string. Copy that string and paste it into a text document – you’ll need it in a moment.

 

## Step 4. Connect to Your Azure Server

### Connect to Your Server

During the server setup under Basics, you have set a username and chosen either SSH key or password.

If you choose an SSH key when configuring your server, you will need to connect to your chosen user name with this key.

If you choose a password, then connect to your chosen username with this password.

The first time you connect to any new server, you’ll be prompted with a security alert about the server’s fingerprint. Click Yes to continue.

 

## Step 5. Run the Provisioning Code

Now, connected to your server, you can complete the final steps.

### 1. Change to the Root User

In my case, I chose the username steve-azure when I created my server, and we can only connect to your Azure instance via this user right now.

However, the GridPane provisioning code needs to be run as the root user. Before running your provisioning code, first paste the following and hit enter:

```
sudo -s
```

Next, cd into the root directory with:

```
cd ~
```

 

### 2. Enter Your Provisioning Code

We’re now running as root and it’s time to paste in the provisioning code that you copied in step 3.

Right-click > Paste and then press Enter. The code will do the rest. A few minutes later, you’ll see the following message in the image below (example taken from our Hetzner article), and you can then close the terminal by typing:

```
exit
```

### Remove Azure System User

If you set up your Azure user with a password, once your server has finished provisioning, connect again and run the following to remove that system user:

```
deluser --remove-home {your-azure-user-here}
```

For example:

```
deluser --remove-home steve-azure
```

 

## Step 6. Wait for Approx 10 Minutes

You can monitor the rest of your server’s provisioning progress inside the Servers page of your account. Approximately 10 minutes later, it will be ready to use inside your GridPane account.

 

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

