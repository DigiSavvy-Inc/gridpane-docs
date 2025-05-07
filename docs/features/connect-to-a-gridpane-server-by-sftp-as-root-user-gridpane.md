# Connect to a GridPane Server by SFTP as Root user | GridPane

# Connect to a GridPane Server by SFTP as Root user

 

2 min read 

With GridPane your servers are your own. You have full access to them and may wish to connect to them as a root user to administer them as you see fit. In this article we will look at how to connect to a GridPane server as root by SFTP to manage files, directories and permissions throughout the entire server.

When you connect as root user you have elevated administrative privileges, therefore you should always be very careful.

 

## Step 1. Ensure you have an Active SSH key

If you haven’t already, then upload your public SSH key to your GridPane settings and add that key to the server you wish to access by SFTP.

We have an easy to follow article that takes you step-by-step through the process of adding an SSH key to a server here.

 

## Step 2. Configure your SFTP client for Root user access

 

 

### Important

**Please note - GridPane only allows SSH Key access to Servers for Root users**

Open your SFTP client and add a new server connection. There are a variety of different and fantastic SFTP Clients for you to choose from, including cross-platform clients such as FileZilla, or the highly recommended Transmit 5 for macOS.

Different SFTP Clients have different interfaces, they are usually very similar but may feature slightly different terminology.

Generally, you will need to select the SFTP protocol, input your server IP address, add your User name, you might need to select your Logon type, and you will need to select the private SSH key that pairs with your System User public SSH Key. Let us look at the two previously mentioned SFTP clients as examples.

### Transmit SFTP Client Connection configuration – SSH Key Log in

Choose SFTP as the protocol, add your server IP in the Server input box, add your username in the User Name input, and either click the key icon to select your private SSH key from your computer directory, before clicking connect. The port is optional but defaults to 22.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1720'%20viewBox='0%200%201824%201720'%3E%3C/svg%3E)### FileZilla SFTP Client Connection Configuration – SSH Key Log in

Choose SFTP as the protocol, then here we see that the server IP input is called Host, you need to set Key File as the Logon Type, enter your username in the User input, and then select your private SSH Key from your computer directory by clicking browse, before clicking Connect. The port is optional but defaults to 22.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2006'%20height='2096'%20viewBox='0%200%202006%202096'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-Root-user/5d77bed08040d.png) 

## Step 3. Manage your Server folders and directories as the root user

As the root user on your GridPane server, you will have full access to the server’s directory structure and filesystem, with complete administrative privileges.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1876'%20viewBox='0%200%201824%201876'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-Root-user/5d77bed1c68a4.png)Remember, with great power comes great responsibility!

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1876'%20viewBox='0%200%201824%201876'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Connect-to-GridPane-Server-by-SFTPs-Root-user/5d77bed35bf4f.png) 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

