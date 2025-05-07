# Connect to a GridPane server by SSH as a System user | GridPane

# Connect to a GridPane server by SSH as a System user

 

4 min read 

 

### Ubuntu 22.04 Servers Only

The information and GP-CLI commands in this article are only applicable to servers running Ubuntu 22.04. For servers running Ubuntu 18.04 or 20.04,  systems user only have SFTP access.

### Table of Contents

 

## Introduction

Our new Ubuntu 22.04 server stack now includes the ability to connect to your servers via SSH as a system user. This is part of a complete rebuild of how system users are handled on GridPane for all future stack updates.

The 22.04 chroot shell is also much more functional and includes:```
awk bash cat clear composer cp curl cut du env find git git-receive-pack git-shell git-upload-archive git-upload-pack grep head id less ls ln mkdir mysql mysqldump mysqloptimize mysqlcheck mysqlrepair mysqlshow mysqlimport mv nano ping php8.0/lsphp80 php8.1/lsphp81 openssl pwd rm sed sh stat strace tail tar tee touch unzip vi wp-cli wc which wget zip
```

By default, system users are still locked to SFTP only, but SSH access can be unlocked to allow access by running a GP-CLI command as the root user. This article covers how to add an SSH key to your system users, unlock SSH access, and then connect to your servers by SSH as a system user.

 

## Step 1. Ensure Your System User Has An SSH Key

This article assumes that you already have a website and you want to use this website’s system user to access your server via SSH. In order to do this, you will need to create a brand new SSH key (you can’t re-use an existing key, so it cannot be the same as the root user), and attach it to your system user.

### Step 1.1 Generate an SSH Key

If you don’t have an SSH Key, please check out the following guides to get started (we like and recommend Termius for both connecting to your servers by SSH and generating SSH keys):

You will need to copy the entire text content of this file to your pasteboard and enter it into the provided Public Key textarea input field. As you can see from the line numbering in the image below, the key is all on a single line, not broken up over multiple lines (a common formatting issue we have seen in the past).

 

 

### Important: Formatting

Please ensure that your key is properly formatted and there is no line break or spaces at the end of the key. Incorrect formatting will break this functionality. Common formatting issues can be found in this troubleshooting article:
Why isn’t my SSH Key working?

### Step 1.2 Add Your SSH Key to an Existing System User

To add your SSH key to your system user, first navigate to the System Users page inside your GridPane account dashboard:

Scroll down the page to the system users table. Here you can search for the system user you want to add your key to:

Click the key icon to open up the modal where you can paste your public SSH key:

Click the Add key button to finish up. Your system user now has an SSH key.

 

## Step 2. Enable System User SSH Access

To enable SSH access on the 22.04 stack, you will currently need to run a GP-CLI command by connecting to your server as the root user. If this is the first time connecting to your servers by SSH, please see these articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Unlock SSH

The following will “unlock” a user so that it can SSH in as the system user (replace {username} with your system users name and don’t include the brackets):

```
gp user {username} -ssh-access true
```

For example:

```
gp user super-awesome-user -ssh-access true
```

### Restrict SSH

You can then lock it down to SFTP only again with the following command:

```
gp user {username} -ssh-access false
```

 

## Step 3. Connect to Your Server by SSH as a System User

Now that you’ve added your SSH key to your system user and enabled SSH access via GP-CLI, you are now ready to connect to your server as your system user.

We like and recommend Termius. This great, free SSH and SFTP client makes connecting to your servers quick and simple and removes the need for manually entering user and SSH key details.

This article has all the details:

Easily Connect to Your Servers with Termius

### Alternatives

Alternatively, if you’ve used a program other than Termius to create your key, you can connect to your server by opening that program (or another of your choosing) and typing the following:

```
ssh {system-user)@{ip-address}
```

For example:

```
ssh [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

Typically, the program used to create the key will set things up so that the shell you’re using knows where to look for your private key. However, if that doesn’t work, you may need to specify the location of your SSH private key like so:

```
ssh -i ~/path/to/your-key {system-user)@{ip-address}
```

For example:

```
ssh -i ~/home/yourusername/.ssh/id_rsa [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

```
ssh -i ~/Users\yourwindowsuser/.ssh/id_rsa [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

