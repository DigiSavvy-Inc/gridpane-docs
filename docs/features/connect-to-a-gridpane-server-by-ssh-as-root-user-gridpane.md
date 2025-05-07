# Connect to a GridPane server by SSH as Root user | GridPane

# Connect to a GridPane server by SSH as Root user

 

3 min read 

## Introduction

With GridPane your servers are your own. You have full, unrestricted access to them and may wish to connect to them as a root user to administer to carry out simple command line tasks, like running our GP-CLI, or following our step by step knowledge base articles. In this article we will look at how to do this.

 

## Step 1. Ensure you have an Active SSH key

This article assumes that you already have a server up and running in your GridPane account. If you haven’t already, then upload your public SSH key to your GridPane settings and add that key to the server you wish to access by SFTP.

We have an easy to follow article that takes you step-by-step through the process of adding an SSH key to a server here.

If you don’t have an SSH key yet, please follow the guides below.

### Generate an SSH Key

If you don’t have an SSH Key, please check out the following guides to get started (we like and recommend Termius for both connecting to your servers by SSH and generating SSH keys):

You will need to copy the entire text content of this file to your pasteboard and enter it into the provided Public Key textarea input field. As you can see from the line numbering in the image below, the key is all on a single line, not broken up over multiple lines (a common formatting issue we have seen in the past).

 

 

### Note

Although you may have named your SSH Key as something other than root when you added it to your GridPane SSH Keys, this naming is for organisational purposes in your GridPane settings only. This key will be added to a server as a root user key and to connect to a server using it you will need to ssh in as root.

## Step 2. Connect to your server as Root via SSH

Now that you’ve added your SSH key to your server, you are now ready to connect to your server as the root user.

We like and recommend Termius. This great, free SSH and SFTP client makes connecting to your servers quick and simple and removes the need for manually entering user and SSH key details.

This article has all the details: Easily Connect to Your Servers with Termius

### Alternatives

Alternatively, if you’ve used a program other than Termius to create your key, you can connect to your server by opening that program (or another of your choosing) and typing the following:

```
ssh root@{ip-address}
```

For example:

```
ssh [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

Typically, the program used to create the key will set things up so that the shell you’re using knows where to look for your private key. However, if that doesn’t work, you may need to specify the location of your SSH private key like so:

```
ssh -i ~/path/to/your-key root@{ip-address}
```

For example:

```
ssh -i ~/home/yourusername/.ssh/id_rsa [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

```
ssh -i ~/Users\yourwindowsuser/.ssh/id_rsa [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

Your local machine will now connect to your remote GridPane server and you will have full access with administrative privileges.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

