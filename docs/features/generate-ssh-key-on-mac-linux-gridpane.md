# Generate SSH Key on Mac/Linux | GridPane

# Generate SSH Key on Mac/Linux

 

3 min read 

 

### Information

Our team and many GridPane users use Termius to connect to their servers. Termius works on Windows, Mac, and Linux. Learn how to generate an SSH key with Termius here:

Generate an SSH Key with Termius

## Introduction

As you get familiar with our platform, you might find that you would like to use SSH and customize your server or use our GPCLI (GridPane Command Line Interface) to make adjustments to your server. We’ve locked down all SSH access to require a SSH key. This article will help you generate and push a key. All you’ll need for this is a Mac or Linux operating system.

### Table of Contents

 

## Getting Started Video

Here’s a video of the process if you would prefer to watch or continue to the written guide below:

 

 

## Step 1: Launch Terminal

Click the finder magnifying glass in the top right corner, type in terminal and click on the application.

 

## Step 2: Generate your key

When you first launch terminal, it’ll be a clear screen. Type in “ssh-keygen -t rsa”. It will then ask you where to save it, it’ll have a default path, and you can just press enter to accept the default path. Next, it will ask you about passphrase. If you put a passphrase in, your key will be encrypted, and when you connect to servers, you’ll have to answer the passphrase. Once you’re done with that, the key is generated.

 

## Step 3: View your public key

Once the key is generated, you can do “cd .ssh” and then “ls”. You’ll see two files listed, an id_rsa file which is your private key (don’t share or upload anywhere!) and then do “cat id_rsa.pub” which is public and safe to upload to GridPane. Select the key, and copy it to your clipboard.

 

## Step 4: Upload to GridPane

Click your name in the top right, and click your settings. Go to SSH Keys, and fill out the add SSH Public Key screen. Name can be whatever you would like it to be. Public key is what we copied in step 3, and then click add key:

 

## Step 5: Push the key to your server

Click on Home in the GridPane UI, and click on the key symbol beside your server:

To add a key, select the key from Available Keys column on the left, and then use the right arrow to add it to your server:

Full details on adding and removing keys from your server can be found in this article:

Add/Remove an SSH Key to/from an Active GridPane Server

 

## Step 6: Connect to your server as root

Within Terminal, type “ssh root@serverip” and hit enter. You may be prompted with an “authenticity” message, and all it means is that your workstation has never connected to the server before. Just type “yes” and hit enter. After that, you should be connected to your server, and can run any GPCLI command you would like!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

