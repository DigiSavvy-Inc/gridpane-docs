# Connect to a GridPane Server by SFTP as System User | GridPane

# Connect to a GridPane Server by SFTP as System User

 

3 min read 

### Table of Contents

 

## Introduction

When we want to download/upload files and folders to our Serious WordPress site we should use SFTP (it’s stronger than FTP), or SSH File transfer Protocol, to securely access our System Users’ sites’ directories.

Want to watch this process? Here you go:

 

## Step 1. Ensure you have an Active System User

You will need to have both added a System User to GridPane and deployed sites as that System User. The System user home directory will be the only directory on the server that you will have access to.

We have easy to follow step by step guides on adding system users and deploying sites here.

You can locate your password for each individual system user on the System Users page here:

 

## Step 2. Configure your SFTP client for System User access

Open your SFTP client and add a new server connection. There are a variety of different and fantastic SFTP Clients for you to choose from, including cross-platform clients such as FileZilla, or the highly recommended Transmit 5 for macOS.

Different SFTP Clients have different interfaces, they are usually very similar but may feature slightly different terminology. Generally, you will need select the SFTP protocol, input your server IP address, add your User name, you might need to select your logon type, and you will either need to select the private SSH key that pairs with your System User public SSH Key or your System User Password. Let us look at the two previously mentioned SFTP clients as examples.

### Transmit SFTP Client Connection configuration – SSH Key & Password Log in

Choose SFTP as the protocol, add your server IP in the Server input box, add your username in the User Name input, and either click the key icon to select your private SSH key from your computer directory or enter your password, before clicking connect. The port is optional but defaults to 22.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1876'%20viewBox='0%200%201824%201876'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-System-User/5d77be6fe235c.png)### FileZilla SFTP Client Connection Configuration – SSH Key Log in

Choose SFTP as the protocol, then here we see that the server IP input is called Host, you need to set Key File as the Logon Type, enter your username in the User input, and then select your private SSH Key from your computer directory by clicking browse, before clicking Connect. The port is optional but defaults to 22.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2006'%20height='2096'%20viewBox='0%200%202006%202096'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-System-User/5d77be715328e.png)### FileZilla SFTP Client Connection Configuration – Password Log in

Choose SFTP as the protocol, then here we see that the server IP input is called Host, you need to set Normal as the Logon Type, enter your System User username in the User input, and your System User password, before clicking Connect. The port is optional but defaults to 22.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2006'%20height='2096'%20viewBox='0%200%202006%202096'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-System-User/5d77be72c255a.png) 

## Step 3. Manage your System User owned WordPress Directories

As a System User you will have full access to your System Users’ home directory on the GridPane server. In this directory you will find all this user’s active sites and their associated staging and update sites.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1876'%20viewBox='0%200%201824%201876'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-System-User/5d77be743c60f.png)Your System Users have sandboxed access to the servers so they may edit and manipulate their associated WordPress sites freely, but they are unable to affect any of the other System User’s WordPress installations on the same server.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

