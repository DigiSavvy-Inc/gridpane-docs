# The Ubuntu 22.04 Stack Feature Updates | GridPane

# The Ubuntu 22.04 Stack Feature Updates

 

4 min read 

 

### Support for Ubuntu 18.04 Servers Ends May 1st 2024

Please ensure you migrate your websites to Ubuntu 22.04 (recommended) or 20.04 servers before this date to continue using support. Please see this guide on how to proceed:
How to Migrate from Ubuntu 18.04 to Ubuntu 22.04

### Table of Contents

 

## Introduction

Our Ubuntu 22.04 release includes some major upgrades to our overall stack. These updates pave the way for continued improvements into the future and, most noticeably from a feature standpoint, now include support for system user-level SSH access. This also means:

We’ll dig into everything below.

 

 

### Migrating From Ubuntu 18.04

For those of you beginning to migrate from Ubuntu 18.04 servers, our cloning scripts are fully compatible with both the 22.04 and 20.04 stacks. However, as with any migration, please ensure you thoroughly test that all your sites have migrated successfully before deleting your original servers.

## System User Updates

The Ubuntu 22.04 stack includes a complete rebuild for how we handle system users. This allows you to access your servers via SSH as well as SFTP. The 22.04 chroot shell is much more functional and includes:

```
awk bash cat clear composer cp curl cut du env find git git-receive-pack git-shell git-upload-archive git-upload-pack grep head id less ls ln mkdir mysql mysqldump mysqloptimize mysqlcheck mysqlrepair mysqlshow mysqlimport mv nano ping php8.0/lsphp80 php8.1/lsphp81 openssl pwd rm sed sh stat strace tail tar tee touch unzip vi wp-cli wc which wget zip
```

To enable SSH access on the 22.04 stack, you can use the settings modal in the UI, or you can run a GP-CLI command by connecting to your server as the root user.

Updates also include:

Details on creating and managing users on 22.04 and future stacks can be found here:

Create and Manage System Users on Your GridPane Servers

 

## GP-Cron Active by Default

On Ubuntu 20.04 and below, GP-Cron needed to be manually activated on a per-website basis.

On Ubuntu 22.04 and all future stacks, GP-Cron is now active on all sites by default, uses WP-CLI, and is fully multisite compatible.

### What is GP-Cron?

WP-Cron is how WordPress handles scheduling time-based tasks such as checking for updates and publishing scheduled post. Our GP-Cron does the same thing, but at the server level, and when GP-Cron is active, we disable the native WordPress cron via your websites wp-config.php file.

However, unlike WP-Cron, which relies on people visiting your website, we set it to run every 5 minutes, ensuring that important tasks are not missed.

You can learn more about GP-Cron and how to customize it in this knowledge base article:

WP-Cron and GridPane’s GP-Cron

 

## Unix Sockets Update

The 22.04 stack is configured to use Unix sockets for both MySQL and Redis connections. This may offer a performance boost for dynamic websites such as WooCommerce, BuddyBoss, LMS, etc.

 

## Redis Updates

In addition to using Unix sockets for Redis connections, Redis also now uses separate database indexes per website.

 

## MySQL Memory Defaults

Our default MySQL memory settings have increased, allowing for more generous memory settings out of the box.

 

## Auto-Configured Plugin Caching Settings

Caching plugins are now auto-configured on activation.

 

## /tmp Lockdown

The /tmp directory is now mounted as noexec. This means that this directory cannot contain executable binaries (and ensures that system users cannot execute code from the /tmp directory).

Originally, this caused issues with the Backblaze B2 backup integration. These issues have now been solved, and Backblaze will work without issue.

 

## Nginx Includes Lua

Our Nginx stack now includes both Lua-Nginx and NJS (Nginx-Javascript) out of the box.

 

## Migrate from Ubuntu 18.04 to Ubuntu 22.04

Please ensure you migrate your websites to Ubuntu 22.04 (recommended) or 20.04 servers before May 1st 2024 to continue using support. Please see this guide on how to proceed:

How to Migrate from Ubuntu 18.04 to Ubuntu 22.04

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

