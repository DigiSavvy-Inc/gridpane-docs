# Provision a Linode Using the Linode API | GridPane

# Provision a Linode Using the Linode API

 

5 min read 

## Introduction

In this article, we’ll be walking through all the steps to get started with Linode and GridPane. We’ll first take a look at getting things set up in your Linode account, and then we’ll provision a Linode server directly from within our GridPane dashboard using the Linode API.

 

## Step 1. Create a Linode Account and Log In

Linode often offers free credits when creating a new account. You can usually find these offers easily through a quick Google search if you don’t already have an account with them.

You’ll need to verify your email address and add your billing info to complete your sign-up. Once complete, log in to your account.

 

## Step 2. Generate a Linode Personal Access Token

Log in to your Linode Account via the new Linode Cloud Control Panel.

Once inside the control panel click on your username in the top right navigation, then select My Profile from the dropdown menu. Your profile page will open, and you now need to select the API Tokens tab.

### Create Your API Token

In the API Tokens panel, you click on the blue Add a Personal Access Token at the top right of the panel.

When you click the link, a configuration panel will slide out from the right side of your browser. Use this panel to configure your token.

Once you have configured the correct Access, click Submit to create your Token.

### Copy your Linode API Personal Access Token

Once you click Submit, the Cloud Console will display your Personal Access token in a pop-up modal. This token will only be displayed once, so make sure to store it somewhere safe.

 

## Step 3. Add Your Linode Token to GridPane

Login to your GridPane account and click the Your Settings menu item in the dropdown menu accessible by clicking on your username and icon.

Locate and click the Integrations option in the left horizontal menu, and then within Cloud Providers select Linode, and then enter your Personal Access Token you copied in Step 2 above into the Token input field, give your key a name, and then click Create.

### View/Edit your Linode API Token

Your Linode API Token will now be available from this settings panel. If you wish to edit or change your API Token, you may do this by clicking the edit button with the blue pencil icon.

A popup modal will appear, and you can easily change your Linode Personal Access Token and click Update.

 

## Step 4. Provision a New Linode Server

Now we have our Linode Personal Access Token saved in our GridPane settings we are able to provision Instances with it from within GridPane. First, navigate to the Servers page in your account:

### Configure Your Linode

Select Linode from the choice of Cloud VPS providers and a configuration panel will open:

Enter an appropriate name for your Linode, and then choose a server plan and region from the dropdown selectors, before choosing whether or not you wish for Linode Backups to be enabled.

 

 

### IMPORTANT

Linode has a character limit when naming servers. This must be between 3 - 32 characters. 33 characters and above the server will fail to provision.

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

 

## Step 5. Wait 10-15 Minutes

GridPane will begin provisioning your instance. You will now be able to see your instance in the Active Servers list.

At any time during the provisioning process, you may check what stage the process is at by rolling over the progress bar, a pop-up window will display the current job being completed.

Once GridPane has finished provisioning your Linode the progress bar will turn green, and you will be able to deploy some Serious WordPress Sites on it.

 

## Step 6: Contact Linode to Unblock SMTP Ports

Linode restricts access to ports that are used for mail delivery via SMTP. Follow this article to get them unblocked for your server.

 

## Congratulations! Next Steps

Now that your server is live, you’re ready to start creating and configuring new WordPress websites.

To deploy a site click on the Sites link in the GridPane main menu to begin the process. We have a separate article that details the steps in detail for you.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

