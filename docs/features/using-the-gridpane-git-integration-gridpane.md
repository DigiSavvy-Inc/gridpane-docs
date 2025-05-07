# Using the GridPane Git Integration | GridPane

# Using the GridPane Git Integration

 

14 min read 

### Table of Contents

 

## Introduction

Git is a professional development tool which allows you develop and update your websites with additional the benefits of version control and a historical record of your code changes.

GridPane offers two different types of Git integrations: Full deployments and Hybrid deployments. In this article we’ll look at how to use Git with your GridPane hosted websites.

This includes both fully automated deployments and manual deployments.

 

 

### Information

Before you begin, please be sure to read this article on the two different types of integrations available and how they are configured:
An Overview of GridPane Git Options: Full and Hybrid Repo Types

Part 1: GridPane Base Repositories

 

## Before You Begin

This article assumes that you’re familiar with and comfortable with the fundamentals of using Git, and that you know how to create and push changes to repositories.

If you’re brand new to Git but are looking for a place to start, please check out this article:

A Beginners Quick Start Guide to Git for WordPress

In part 3 you’ll also find links to two intro videos that also demonstrate the fundamentals

 

## Download GridPane’s Base Full and Hybrid Repositories

Before you attach a repository to GridPane, you need to first make sure that your file structure is set up correctly. To assist with this, we’ve created three base repo’s that you can fork and use to create your own repos. Learn more about repo types here.

### 1. Full Repository: All GridPane Plugins

This repo contains all of our mu-plugins, which include wpFail2Ban, our SSO plugin, caching plugins, etc. This is an example of a properly configured repo for a site with all our app settings enabled that require these plugins.

You can view/fork/download the full repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-template-all-pluginsBranch: main

### 2. Full Repository: Basic

This repo is essentially an empty repo with only what you need to begin using our Git integration. You can view/fork/download the full repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-templateBranch: main

### 3. Hybrid Repository

You can fork/download the hybrid repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-hybrid-templateBranch: main

### Additional Info

Each of the repos contains extensive README.md files on how to work with these repos and our Git integration.

These repos are automatically kept up to date with the latest WordPress version.

 

 

### Important

Please ensure that your repository does not contain a wp-config.php file. As with regular sites at GridPane, this is stored one level up from the /htdocs directory, and a competing wp-config.php can cause strange behavior and break your sites. Learn more here:
Working with the wp-config.php on GridPane and an introduction to user-configs.php

## Public vs Private Repos

Both public and private repos will work with GridPane. These are exactly what they sound like – a public repo can be viewed and forked by anyone, and a private repo can only be seen by you and those you give access to.

Using public repos is a simple process – all you need is the public URL and you’re all set.

Private repos require more initial setup.

If you’re using any premium plugins or themes, you’ll most likely want to use a private repository. You can learn more about configuring Git repositories for your GridPane websites in this article:

How to Configure Git Repositories for GridPane Hosted Websites

 

Part 2: Connecting Your Websites to Git

 

## 1. Add a Repo and Branches

Inside your GridPane dashboard, navigate to the Git page. Here you can add your Git repositories and branches (you will need to add at least one branch in the beginning, but you can easily add more in the future).

Next, add your repo. Please note that:

Fill in your repository name, repository URL, and Git branch name, for example:

If you would like to add additional branches, click the Add another branch button. Once you’ve entered all your details, click the Add Git repository button.

Once added, you can see and manage your different branches in the Active Git Repository Integrations section below.

### Self Hosted Git

If you’re using a self-hosted version of Gitlab, GitHub, or Bitbucket, please select the corresponding self-hosting setting. For example:

 

## 2. The Git Integration Manager

On the Git page in your account, click the cog to open the manager:

It looks as follows:

Here you can update the integration name, copy your webhook, and if no sites have been connected to the repository yet you can also update the URL.

On the Deployed Branches tab, you can manage the branches associated with the repo.

On the Connected Sites tab, you can connect sites and manage their deployments.This means you can manage all sites connected to a repo across the entire dev workflow that repo represents from one place. More details on deployments can be found in part 3 below.

 

## 3. Connect a Site to Your Git Repo

There are two different ways to connect your websites to a Git repository. It can be either through the Git Integration Manager or directly via the website’s customizer on the Sites page of your account.

 

### Connect Site Using the Git Integration Manager

As illustrated in the previous section, open up the Git Integration Manager for your repo, and then open the Connected Sites tab.

Here, click the Connect Site button and select the site and the branch you want to use.

Once you’ve connected a website you will see the UI update with the following details:

##### The Deployment Webhook

Now that you’ve attached a site, copy the Deployment Webhook to get the token for automated deployments. This token applies to all branches.

If you ever need to, you can click the regenerate button to create a new token and new webhook (though note that this will stop the old webhook from working).

##### Deployment Information

You’ll also see the following:

This information can also be seen inside your website customizer in the Git tab – details below.

 

### Connect Site From the Website Customizer

To get started, head over to the Sites page inside your GridPane account, and click on the website to open up the website customizer:

Inside the Configuration tab, you can select the branch from the dropdown and then click the Attach Repository button.

Once you have connected your site to your repo you will see:

These settings will match up inside the Git Integration Manager row for the site (see the previous section above).

##### The Deployment Webhook

Copy the Deployment webhook for automated deployments.

If you ever need to, you can click the regenerate button to create a new token and new webhook (though note that this will stop the old webhook from working).

##### The Deployments Tab

You will also see a deployments tab which will be empty of entries initially. Entries will include:

This tab will contain the entire history of deploys for a site once it has been configured for Git.

The deployment history is also available from the Git integration manager row for the site.

Here’s an example preview:

 

## 4. Disconnecting a Website from Git and/or Removing a Repo

If you would like to disconnect a website from Git or remove a repository from your account, this is a simple process.

### Disconnecting a website from Git

If you would like to remove a website from an integration you can click the disconnect icons present in both the website customizer:

Or the Git Integration Manager, inside the Connected Sites tab:

### Removing a Branch or Repository

You can only remove branches and repos if there are no websites connected to them. This option will remain locked until the connections to sites are removed.

To remove a repo, head over to the Git page inside your account, locate the name of the branch you wish to delete (you can use the search box if you have a lot of repos attached), and then click the delete icon:

To remove a branch, open up the Git Integration Manager and you’ll see a delete icon on the right-hand side next to each of your branches – click it to remove the specific branch:

 

Part 3: Git Deployments

 

## 1. Run Manual Deployments

Manual deployments can be run from:

If you want to redeploy any previously deployed commit then you can also do this in both of these locations as well.

 

### Run a Manual Deploy from the Git Integration Manager

On the Git page in your account, open the Git Integration Manager, locate the Deploy Now button, and click it to start your deployment:

Once clicked, the button will turn into a spinning icon and the deployment will start running, and other data fields will update as the deployment calls back.

Once the deployment has completed you will see all the fields populated and the state of the last deployment. Assuming all went well and you will see a green timestamp.

If the deployment was unsuccessful for any reason you will see a notification and no changes will be made to your website.

 

### Run a Manual Deploy from the Site Customizer Git tab

Over on your Sites page, click on your website to open up the site customizer and click through to the Git > Deployment tab, locate the Deploy Now button, and click it to start your deployment:

Once running a new row will be created in the deployments table.

You can click the right-facing arrow at the end of the row to open up the deployment log at any time.

If you want to redeploy any previously deployed commit, then you can click the redeploy now button (which is the cloud button with an upward arrow).

If the deployment was unsuccessful for any reason, you will see a notification and no changes will be made to your website.

 

## 2. Run Automated Deployments – Push to Deploy

### Step 1. Get Your Push to Deploy Webhook

You can find your webhook over on the Git page Git Integration Manager, or the Sites page inside the website customizer > Git tab.

You will see the Git deployment hook with a copy/paste symbol. If you click on this it will copy your deployment webhook to your pasteboard, for example:

```
https://my.gridpane.com/api/site-git/deployments/4f478219-1234-abcd-a829-b3d1b47ol473
```

 

### Step 2. Add your webhook to your Git repo

At your hosted Git provider there will be a section to configure the platform to hit a webhook whenever an event such as a push to your repo occurs.

For demonstration purposes, we will use GitHub as an example.

Go to your Repo > Settings > Webhooks and click add webhook:

Add the webhook you copied and click add webhook:

You can have things set to JSON or URL encoded, andall the default settings should be fine.

Once added you may see that the platform attempts to make a call to the webhook and is showing an error. Don’t worry, that is just because we haven’t enabled the deploy webhook at GridPane yet.

 

### Step 3. Enable Push to Deploy at GridPane

You can enable push to deploy in either the Git Integration Manager > Connected sites tab > Deploy toggle:

Or the Site Customizer > Git tab > Configuration tab > Enable automatic deployments on push to origin toggle:

Toggle either of those on and you’ve successfully set up automatic Git deployments for your website.

 

## Checking Your Deployments

As with the previous sections, you can check your deployments in both the Git Integration Manager and your website customizer. You can also see previous deployment history inside the integration manager.

### Check Your Deployment History and Log via the Git Integration Manager

Over on the Git page open up the Git Integration Manager and then the Connected Sites tab. Here you will see the last deploy with a timestamp, and next to that is the history column. Click on the icon next to the site you want to check to open up the history modal:

This will display your previous deployment history for the site. Over on the right hand side you can also open up the deploy log by clicking on the arrow icon:

The log will then display in its own modal:

 

### Check Your Deployment Log via the Website Customizer

Over on the Sites page, open up your Website Customizer > Git Tab > Deployments.

Here you will see the last deploy with a timestamp, and  an arrow over on the right hand side. Click on the arrow to open the last deploy log (see image above).

 

Part 4: Git and GridPane Features

 

## Git and Cloning/Staging

Below details how websites that are configured for Git will work with our cloning and staging features.

### 1. The Source site is configured for Git

If the source site of any cloning action is configured for GridPane Git the cloning process will still correctly.

The process will:

Basically, cloning will work just as it does for regular websites.

### 2. The Destination site is configured for Git

For Cloneover and Staging pushes, if the destination site is configured for Git the application/API will only allow DB/settings clones.

Using these together a developer can use Git repos and branches to work on different variants of a WordPress website as part of a development workflow such as gitflow.

Git manages the files. The clone/staging push moves the data and webserver settings.

 

## Git and V2 Backups

When restoring a backup on a Git-configured website, you’ll be presented with different restore options compared to regular WordPress sites.

When restoring non-Git backups to websites that are now configured for Git, we will add the necessary files (where applicable) to your website to ensure it continues to function according to your backup restore choice.

### Backups and Git Full

Similar to cloning and staging, restoring backups for websites configured for Git Full will restore both the database and the uploads directory. This skips restoring the WordPress codebase, which is always the same for every website on the server.

When restoring backups, you have the following 5 options:

Backups are tagged with GPGitSiteFull.

### Backups and Git Hybrid

When restoring backups on Hybrid Git sites, you have the following 5 options (the first 2 differ from Git Full):

The first 2 options won’t replace the files in your Git repo.

Backups are tagged with GPGitSiteHybrid.

 

## Git, Caching, SendGrid, and GridPane Security

Some of our features make use of WordPress plugins. In order for these two function correctly, it’s important that they be included as our systems will check for these plugins to be present for the corresponding functionality to be activated from within your account.

Full details on this can be found in our Git repo configuration article here:

How to Configure Git Repositories for GridPane Hosted Websites: GridPane Plugins and Full Repos

You can also download our base Full that includes all of these plugins here:

https://github.com/GridPane-Dev/gridpane-wordpress-template-all-plugins

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

