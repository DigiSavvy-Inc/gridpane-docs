# Getting Started with the Client Portal (PanelPress.io) | GridPane

# Getting Started with the Client Portal (PanelPress.io)

 

7 min read 

### Table of Contents

 

## Introduction

PanelPress.io is the home of the GridPane Client Portal, a simplified, cleaner, and more “client” friendly UI. The standard “nuclear reactor” UI that is my.gridpane.com can be overwhelming, especially for clients and team members who are not WordPress developers. Now you can provide them access to an interface that is more akin to a managed WordPress host.

The Client Portal allows you to invite your clients and/or team, limit exactly what features they can access and control, and view all of their activity. Depending on your plan, you can also completely white label the whole experience.

In this article, we’ll take a quick walkthrough of the available options and where they live inside of PanelPress. The screenshots below were all taken using dark mode, but you have the option for a light mode as well if that’s your preference.

For a full introduction to why we built the Client Portal, here’s our announcement blog post: Officially Introducing PanelPress.io: The New GridPane Client Portal

 

## Part 1. Sign Up

If you have a Developer or Agency account, you can sign up for PanelPress over at: https://panelpress.io/

The sign-up process will walk you through everything you need to attach your PanelPress account to your main GridPane account.

 

### Personal Access Token

You will need a personal access token to complete the signup process. The portal will also provide the necessary instructions, but for quick reference, you can create a personal access token inside your main GridPane account settings page under GridPane API:

I’ve named my own access token “PanelPress” for easy reference.

 

## Part 2. Add and Manage Sites

PanelPress connects directly to your main GridPane account and allows you to import only the specific sites that you want to do so. You can add, manage, and remove sites from inside the Sites tab in the left-hand sidebar.

You will be able to add additional sites in the future for an additional fee.

 

### Manage Sites

When logged into your account you’ll automatically land on the Sites tab.

To begin importing your sites, click the Manage Sites button in the top right:

This will bring you through to a page that lists all of the websites in your main GridPane account. You can also manually sync with your account if ever needed by clicking the Sync button in the top left of this page.

To import your sites, simply click the Import button on the right in the import/remove column:

Here you can also remove sites here in the future if you ever wish to do so:

Note that removing sites inside of PanelPress does not remove/delete them inside your main GridPane account.

 

### Customize Sites Table

Now that you’ve imported one or more sites, you can customize what info you can see at a glance in the Sites table.

Click the Edit Table button in the top left:

You will be presented with a list of options to display in your table. For example, here I’ve selected some additional options: SSL, caching, server type, and PHP version:

Once you’ve made your selection, click the Update button. You will now be able to see the status of these settings within your site’s table:

 

### Manage Individual Website Settings

Inside of PanelPress, you can manage many of your site-specific settings, with more options to come in the future. You can also limit access to these settings using the Role Editor which we’ll look at in Part 3.

To manage your individual sites, simply hover over them and click to select them from the Sites table. You’ll be presented with multiple additional tabs to manage your different available settings:

Below is a rundown of the available features. Please note that OpenLiteSpeed currently has fewer options than Nginx, but this will be updated in the future.

#### Manage

The manage tab will give you a quick overview of your current PHP version, SSL, and page caching options, as well as your datacenter region.

In the top right, you can make use of SSO to log in to the website.

You can also access your database via PHPMyAdmin and view your SFTP details here.

#### Domains

The domains tab provides an overview of any alias or 301 domains you’ve attached to your site. You can also add additional domains, and toggle SSL on or off for your domains.

#### Infinite Staging

Infinite Staging allows you to connect your site to any other of your sites and create your own custom staging/development workflow.

This means you can chain 3 or more sites together to create an extended workflow, and use non-staging sites as a part of your staging workflow.

#### Tools

Under tools you can manage your caching settings, clear your caches, and change the page cache TTL.

You can also change the PHP version and enable/disable WordPress debug.

#### Backups

The backups tab allows you to view your site’s available backups, restore or purge backups, and manually create backups.

#### Logs

The logs tab allows you to view your error, access, and debug logs. You can also search these logs.

 

## Part 3. Add and Manage Users

The Users tab will allow you to invite new users, manage existing users, and create roles for them.

 

### Managing Users

Here you’ll see any users that you’ve invited to your account.

You can invite new users by clicking the Invite Client button in the top right.

As the primary admin of the account, you’ll see that you can’t delete your own account, but you can easily remove any of your other users from this tab.

 

### Manage Invites

Here you can view and revoke the invites that you’ve sent. To remove an invite, simply click the Delete button.

 

### Activity Log

The activity log allows you to view all of the activity that’s taken place inside of your account.

This includes all of the individual actions that both you and your team/client users have taken.

 

### Role Editor

The Roles tab allows you to add and edit new roles for your team and clients.

This allows you to fine-tune exactly what features and websites they have access to.

To create a new role click the Add Role button to get started:

You’ll be asked to give your role a name, and then you’ll be able to add websites and users to this role.

Next, you can specify exactly what permissions you want this role to have:

You can also copy permissions from other existing roles to speed up the process by clicking the Copy Permissions From button in the top right above the option toggles.

 

## Part 4. Customize Your Account / White Label Options

As the Client Portal continues to develop, more and more customization options will become available.

The white label aspects of the client portal are available on the Agency plan.

 

### White Label Options

The white label options allow you to:

 

### Integrations

Inside Integrations, you can update your GridPane API token if you ever need to do so.

Here, Agency users can also add their custom JS to their account. This is particularly useful if you want to add your own support/chat widget.

 

## Part 5. Account Details

Below is a quick rundown of other options you’ll find in your account. In the top right-hand corner, you’ll see multiple icons and your profile avatar:

 

### Profile Settings / Sign Out

If you click on your avatar in the top right, here you can choose to edit your profile or sign out of your PanelPress account.

Inside your profile settings, you can enable 2-factor authentication for your account, and update your name, email, and avatar.

Correction: Unlike the community forum and support desk which are directly tied to your main GridPane email, your email address inside of PanelPress is not linked to your main GridPane and so you can use a different email address if that’s your preference.

 

### Dark Mode

You have the option to choose between light or dark mode when using your account.

 

### Client Portal Changelog

You can keep up to date with new features, improvements, and bug fixes that are specific to the Client Portal by clicking the rocket icon next to your profile in the top right.

 

### Notifications

You can view notifications associated with your websites by clicking the bell icon next to your avatar in the top right.

Your notifications will only contain actions that have been taken on your websites. They won’t contain notices specific to your servers.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

