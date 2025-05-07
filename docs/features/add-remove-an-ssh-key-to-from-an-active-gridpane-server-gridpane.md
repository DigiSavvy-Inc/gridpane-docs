# Add/Remove an SSH Key to/from an Active GridPane Server | GridPane

# Add/Remove an SSH Key to/from an Active GridPane Server

 

3 min read 

## Introduction

If you wish to securely access your server by SSH or SFTP then you will need to add your Public SSH key to it. GridPane makes it easy to add or remove your SSH Key to any Active Server.

### Table of Contents

 

## Adding SSH Keys to Your Account

### Step 1. Go to Your GridPane Settings

Login to your GridPane account and click the Your Settings menu item in the dropdown menu accessible by clicking on your username and icon.

 

### Step 2. Add your Public SSH to the GridPane SSH Keys settings panel

Locate and click the SSH Keys option in the left horizontal menu, and then paste your Public SSH Key in the Add SSH Public Key panel and click Add Key. You should name this key, since the key will be used for root access to your server I would suggest calling it the root key.

Once you have successfully added your public key it will be listed in the Active SSH Keys panel. 

## Mark your SSH Keys as Default (optional)

GridPane has a Default SSH Keys feature which allows you to add your keys to any servers you provision automatically.

We have an easy-to-follow guide to help you enable this feature here.

 

## Deleting SSH Keys from your Account

To delete a key, head to your Settings > SSH Keys in your account.

Here you’ll see your keys you can click the delete button beside the key you wish to delete inside the panel:

This will open up a modal for you to confirm you want to delete that specific key. If the key is active on any of your servers, you’ll see the following notice:

Click the Remove from all servers button to first have the application remove the key from any servers it’s still currently active on. It’s not possible to delete a key while it’s still on one or more of your servers.

The Delete key button will be available and you can then confirm and delete the key:

 

## Team Members and SSH Keys

Before we start adding keys, it’s important to note a few things with regards to your team member accounts adding SSH keys.

Team Members can only manage SSH keys for your account when working inside one of your teams when logged into their account.

And you of course can add and remove any keys that your team members add to your account. You can learn more about teams here:

Using GridPane Teams

 

## Adding/Removing SSH Keys to/from a Server

### Step 1. Go to the GridPane Home page

The list of Active servers is located on the GridPane home page. Click Servers from the GridPane main menu to navigate there:

 

### Step 2. Locate and Click the Add/Remove Public SSH Keys button

In your Active Servers panel click the Add/Remove Public SSH Keys button located to the right of the server row. The button has a key icon:

 

### Step 3. Add and/or Remove a Public SSH Key

A pop-up modal will appear containing checkboxes for all of the Public SSH Keys available from your GridPane Settings.

To add a key, select the key from Available Keys column on the left, and then use the right arrow to add it to your server.

To remove a key, select it from the Keys on Server on the right, and use the left arrow key to remove it from the server.

 

## Connect to your Server by SSH / SFTP as root user

Now you can connect to your server as root user to either perform administrative tasks and manage the files and directories by either SSH or SFTP.

We like and use Termius and we have a knowledge base article on how you can too:Easily Connect to Your Servers with Termius

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

