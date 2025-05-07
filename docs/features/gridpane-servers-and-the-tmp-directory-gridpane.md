# GridPane Servers and the /tmp Directory | GridPane

# GridPane Servers and the /tmp Directory

 

2 min read 

 

### Ubuntu 22.04 Servers Only

The information and GP-CLI commands in this article are only applicable to servers running Ubuntu 22.04. For servers running Ubuntu 18.04 or 20.04, the /tmp directory is not locked down.

### Table of Contents

 

## Introduction

The GridPane Ubuntu 22.04 stack has the /tmp directory locked down by default. Our scripts, by design, can still handle this internally for things like apt package manager etc, so that your server can still run smoothly.

However, if you install any third-party applications on your servers, it’s possible that they may require /tmp to be executable. In these cases,  you have the option to either work out a configuration for them that replaces the use of /tmp or you can disable the lock.

 

## About the /tmp Directory

The /tmp (temporary) directory belongs to the root user and is used to store temporary files (data that’s only needed for a short period of time) required by the server OS and other installed applications. This includes your WordPress websites.

As an extra security hardening measure, on Ubuntu 22.04, we lock this down by mounting it as noexec. This means that temporary files can still be stored here, but executing binary files from here is not possible. While this lock is active, if any of your sites are ever compromised, malicious processes can’t be run via /tmp.

Additional note: The /tmp folder is typically emptied each time the server is rebooted.

 

## How to Lock and Unlock /tmp With GP-CLI

Locking and unlocking the /tmp directory is quick and simple but currently does require you to connect to your server via SSH. If this is your first time connecting your servers, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

You can disable the lock with the following GP-CLI command:

```
gp server -tmp-noexec disable
```

And if you want to lock it down again, you can run the following command:

```
gp server -tmp-noexec enable
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

