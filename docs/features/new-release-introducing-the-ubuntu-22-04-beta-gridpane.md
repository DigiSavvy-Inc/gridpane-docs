# New Release: Introducing the Ubuntu 22.04 Beta | GridPane

# New Release: Introducing the Ubuntu 22.04 Beta

 

6 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='675'%20viewBox='0%200%201024%20675'%3E%3C/svg%3E)

### Table of Contents

 

## Introduction: The 22.04 Stack Has Arrived

Our brand new Ubuntu 22.04 stack has arrived, and it is available for both Nginx and OpenLiteSpeed. This has been in the pipeline for a long time (with delays being due to waiting for 3rd party packages we use not supporting 22.04) and includes some major upgrades to our overall stack.

These pave the way for continued improvements into the future and, most noticeably from a feature standpoint, now includes support for system user-level SSH access. This also means:

We’ll cover the big updates in more details below, and full documentation will be available soon.

 

 

### Beta Status

The beta is available to everyone on the platform. Please don't use it for critical production websites until its full release. How fast we can move from beta into full production will depend on user testing and feedback alongside our internal testing procedures. The beta is currently only available on Vultr.

## New: System User SSH Access

The Ubuntu 22.04 stack includes a complete rebuild for how we handle system users. This allows you to access your servers via SSH as well as SFTP.

The 22.04 chroot shell is much more functional and includes:

```
awk bash cat clear composer cp curl cut du env find git git-receive-pack git-shell git-upload-archive git-upload-pack grep head id less ls ln mkdir mysql mysqldump mysqloptimize mysqlcheck mysqlrepair mysqlshow mysqlimport mv nano ping php8.0/lsphp80 php8.1/lsphp81 openssl pwd rm sed sh stat strace tail tar tee touch unzip vi wp-cli wc which wget zip
```

To enable SSH access on the 22.04 beta stack, you will currently need to run a GP-CLI command by root. This will “unlock” a user so that can SSH in as the system user:

```
gp user {username} -ssh-access true
```

You can then lock it down to SFTP only again with the following command:

```
gp user {username} -ssh-access false
```

 

## Stack Info and Available PHP Versions

The 22.04 stack only supports PHP 8.0 and 8.1. As PHP 7.4 reached its end of life in November 2022, it will not be included or supported on new stacks moving forward.

PHP 7.3 and 7.4 are still available on the Ubuntu 20.04 stack for any sites that are not yet compatible with PHP 8 and above.

### Nginx Stack Info

### OpenLiteSpeed Stack Info

 

## The /tmp Directory and Backblaze B2

The 22.04 stack has the /tmp directory locked down by default.

We handle this internally for things like apt package manager etc.

If you install any third-party applications on your servers, it’s possible that they may require /tmp to be executable. In these cases,  you have the option to either work out a configuration for them that replaces the use of /tmp or you can disable the lock.

You can disable the lock with the following GP-CLI command:

```
gp server -tmp-noexec disable
```

And if you want to lock it down again, you can run the following command:

```
gp server -tmp-noexec enable
```

### Backblaze B2 Remote Backups

Our B2 backups currently won’t work out of the box on this stack without disabling the /tmp lock. This is because Backblaze uses the /tmp directory for executables.

We are currently looking for a workaround for this, but if we find that this is not possible, then it will be up to you to decide between the lock and B2 backups.

More information will be available inside the knowledge base in the near future.

 

## Q&A

 

### How do I upgrade from 18.04/20.04 to 22.04?

When the 22.04 stack is moved out of beta and into full production, the easiest way to move your websites is to create a brand new server and then use our full server clone functionality. Details on this feature can be found here:

Cloning One Entire Server to Another

Unfortunately, there’s really no way to support upgrading a server’s OS. This is not the straightforward process that it appears to be on the surface, and it can’t simply be automated. Hiring a sysadmin to manually upgrade the OS of a live production server would be no small investment.

Each stack is built specifically to be compatible with each version of the Ubuntu OS and the different software/packages/modules that support it.

 

### Can I clone sites from 18.04/20.04 servers to 22.04?

Yes, assuming your servers are all properly sized, and your website databases don’t have any serious issues.

If you’re running a full server-to-server clone, you will also be able to use remote backups from alternative sources for any that don’t play nice for any reason.

 

### Why can’t you support new Ubuntu releases as soon as they come out?

There are numerous reasons why support for new OS versions takes some time. For example, we were waiting for specific Nginx updates before we released the 20.04 stack, and then ultimately ended up building those ourselves.

Here’s a rundown of the different factors:

Future stacks will continue to build upon the previous ones, and these may not always have such huge changes like the new system user functionality and directory structures, but we will always be at the mercy of the 3rd party packages we use, which can take 6-9 months or more to come out after the LTS release date.

 

 

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

### 2 Comments

## Leave a ReplyCancel Reply

Your email address will not be published. Required fields are marked *

Name  *

Email  *

Website

Please check the box below to consent to the processing of the submitted personal data in accordance with our Privacy Policy, including the transfer of data to the United States.

I have read and accepted the Privacy Policy
		 *

Add Comment *

Post Comment

 

 