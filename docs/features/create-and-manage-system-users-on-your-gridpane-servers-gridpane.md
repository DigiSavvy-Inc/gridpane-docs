# Create and Manage System Users on Your GridPane Servers | GridPane

# Create and Manage System Users on Your GridPane Servers

 

7 min read 

## Introduction

System users are an important part of your WordPress security systems. Unlike most traditional hosting where all of the websites on your account are owned by one individual system user, GridPane makes it extremely easy to add each of the websites you host to their own, individual system users.

### Table of Contents

 

 

### System User SSH Access on Ubuntu 22.04

The Ubuntu 22.04 stack includes a complete rebuild for how we handle system users. This allows you to access your servers via SSH as well as SFTP.

The 22.04 chroot shell is much more functional and includes:
awk bash cat clear composer cp curl cut du env find git git-receive-pack git-shell git-upload-archive git-upload-pack grep head id less ls ln mkdir mysql mysqldump mysqloptimize mysqlcheck mysqlrepair mysqlshow mysqlimport mv nano ping php8.0/lsphp80 php8.1/lsphp81 openssl pwd rm sed sh stat strace tail tar tee touch unzip vi wp-cli wc which wget zip
To enable SSH access on the 22.04 stack, you can use the settings modal in the UI or you can run a GP-CLI command by connecting to your server as the root user.

## Always Use One System User Per Website

There are three important reasons for always keeping each of your websites on their own system user.

### 1. Security

This keeps each of your websites completed isolated from one another at the server level, and should any of your sites ever be compromised, that specific site cannot cross-contaminate the other websites on your server.

If you’ve ever been the victim of malware, you know just how important this is for your security (and your sanity).

### 2. Limit Access

Beyond security, one site per system user also allows you to give client/developer SFTP access only to the website that they own and need access to, and not all of the sites on your server. This way the client has sandboxed access to their site’s WordPress directory and database only, and cannot affect any other part of the server.

### 3. Resource Monitoring

You can also use system users to identify when a site is consuming a high amount of resources on your server with the top and htop commands over the command line.

 

## Option 1. Create a New System User When You Create a New Website

GridPane allows you to easily create new system users at the same time you create new websites over on the Sites page of your account.

Once you’ve entered your URL and selected your server you’ll be able to:

When you proceed to create your site, we’ll handle the rest.

You can learn more about this and how to set your default options for creating new websites here:

New WordPress Website Build Configuration Settings

All of the information below covers the manual creation of system users over on the System Users page inside your account and will help you create new system users for websites that you clone/migrate if needed.

### Creating New WordPress Websites

We have a separate article that guides you step by step through the GridPane site deployment process here.

 

## Option 2. Create a System User on the System User Page

Navigate to the System Users page inside the GridPane control panel by clicking on the link in the top menu bar:

Assuming you have already provisioned a server you can add a system user. It is very straightforward, all you need to do is configure your System User credentials and then allocate it to a GridPane server.

### Create a new user on Ubuntu 20.04

On Ubuntu 20.04 and below, you can give your new system user a custom name, custom password, and add an SSH key.

The user creation settings look as follows:

### Create a System User on Ubuntu 22.04

On Ubuntu 22.04 and all future stacks, you have additional options for choosing the system user type.

#### 1. Create a chrooted system user:

This user can be used to take ownership on new and existing websites, and you can choose whether this user has SFTP only access to your website, or both SFTP and SSH access.

#### 2. Create a non-chroot sudo user:

### Step 1. Choose a Username

When choosing your System User name, remember this is a linux username so there can be no whitespaces only letters, numbers, and characters.

### Step 2. Choose a secure password

Next enter a secure password for your system user, and then confirm the password.

 

 

### Password Restrictions

System users have strict password validation settings, and new passwords will need to meet the following criteria:

16 characters minimum
1 Uppercase minimum
1 Lowercase minimum
Numeric minimum
Symbol minimum

### Step 3. Add your SSH Public Key (Optional)

Lastly add your Public SSH Key if you plan to access your domain over SFTP via this system user. If you don’t have an SSH Key, please check out the following guides to get started:

You will need to copy the entire text content of this file to your pasteboard and enter it into the provided Public Key textarea input field.

When you add your Public SSH Key, please make sure that there is no newline following the last character of the key.

The following is good and the key will work:

This is bad and the key will not work:

 

 

### Note

You can enter either a Password or a SSH Key, both are optional but you must enter one. If you are creating sites for a client, it may be advisable to use your SSH key, and provide your client with the password.

### Step 4. Create Your New User

Once you’ve completed the necessary fields, click Add user to create your system user.

Your new user will now appear in the dashboard below the Add System User panel.

### Provision WordPress sites with your System User

Now it is as simple as choosing your system user from the System User dropdown selector when you provision sites on your server as detailed in the previous section here.

 

## Managing Existing System Users

All of your system users can be managed directly on the system users page.

If you’re looking to manage the user of a specific website, once your site has been provisioned, you will see your System User in the user column of the site in the Active Sites panel.

You can then manage this and all your system users on the System Users page in your account. Here you can change its password, add or change an SSH key, view your user’s password, and delete it.

You can use the search box to find your user, and then on the right hand site you have 3 buttons available:

These do the following:

### Update System User Settings

The settings configuration modal looks as follows (note that on Ubuntu 20.04 servers and earlier stacks, the two SFTP and SSH access options under “Public Key” will not be displayed):

Here you can update the password and/or SSH key.

On Ubuntu 22.04 and future stacks, you can also unlock or remove SSH access for this user.

### Enable/Disable System User Access with GP-CLI

You can also use GP-CLI to “unlock” a user so that they can SSH in as the system user.

Connect to your server via SSH as the root user and run the following commands (replace {username} with your system users name and don’t include the brackets) to enable or disable access:

```
gp user {username} -ssh-access true
```

You can then lock it down to SFTP only again with the following command:

```
gp user {username} -ssh-access false
```

### Deleting Users

When you go to delete a user, you will need to reassign any sites that it currently owns to a new user before you can proceed:

Once the websites have been re-assigned, the Delete User button will become available.

UpIf you need to change a website from one system user to another, you can check out this article.

 

## Access your System users sites via SFTP

Now you can access your system users home folder via SFTP, using either a SSH key pair or password, to upload/download and update the sites directories and files.

We have a separate article that takes you step by step through the process of accessing GridPane sites by SFTP as a System User here.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1824'%20height='1720'%20viewBox='0%200%201824%201720'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Add-System-User-to-GridPane-Server/5d77bede669c5.png) 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

