# How to Use GP WP-CLI and Regular WP-CLI on GridPane Servers | GridPane

# How to Use GP WP-CLI and Regular WP-CLI on GridPane Servers

 

4 min read 

### Table of Contents

 

## Introduction

This article digs into how to use WP-CLI commands on your GridPane servers. By default, WP-CLI is installed on all GridPane servers out of the box and you

However, before you begin, be sure to read through the information below to understand how it works, and why we created GP WP-CLI.

In the last section we’ll take a look at some useful  WP-CLI commands.

 

### What is “GP WP-CLI” and Why Does it Exist?

Good question. Currently, GridPane servers are locked down by SSH to root users only, which somewhat curtails WP-CLI and leads to a few gotchas.

It means that WP-CLI can only be run as the root user using the --allow-root flag with every command.

This means that any file changes that occur during your running of the WP-CLI command will have a permissions error as they will belong to the root user and not the site system-user. It also means WP-CLI is running as root, which can be insecure if your site is already, unbeknownst to you, compromised.

It also means things like the WP-CLI configurations per system user are unavailable. This means, amongst other things, you need to navigate to the path of the WordPress installation or provide the path to htdocs with the --path=/var/www/{site.url}/htdocs flag.

So as a part remedy to this we developed a GP-CLI wrapper for WP-CLI. It can navigate our security settings and run the WP-CLI commands as the correct system user.

 

## Using GP WP-CLI

GP WP-CLI doesn’t require a filepath providing, nor does it need to be run from within the site’s /htdocs directory.

Commands can be run for any website from anywhere on the server.

### File Creation

That said, it does need to have a full path for any file created (for example, when exporting a database) and the destination of the file needs to be in a location writable by the sites php system user. Your website’s htdocs folder –/var/www/{site.url}/htdocs – is the easiest option for this.

If you are running the command from root and not passing an explicit full path for the output, it will try to create the file in a location that is inaccessible.

 

## GP WP-CLI Syntax

The syntax is as follows:

```
gp wp {site.url} {wp.cli.command} {arg} {arg} {arg} {arg.n}
```

You will replace {site.url} with your site’s primary domain, {wp.cli.command} with the WP-CLI command you wish to use, and then pass all the subcommands or arguments you would use with wp-cli sequentially afterward.

### Example 1

So, for example, the following WP-CLI plugin command:

```
wp plugin install hello-dolly --activate 
 --path=/var/www/an-example.site/htdocs --allow-root
```

In GP WP-CLI is:

```
gp wp an-example.site plugin install hello-dolly -activate
```

### Example 2

The following WP-CLI database search and replace command:

```
wp search-replace an-example.site an-example.website 
 --dry-run --precise --all-tables --skip-columns=guid 
 --report-changed-only --path=/var/www/an-example.site/htdocs --allow-root
```

In GP WP-CLI is:

```
gp wp an-example.site search-replace an-example.site an-example.website 
 --dry-run --precise --all-tables --skip-columns=guid 
 --report-changed-only
```

Obviously this is shorter, but it also has the advantage of allowing us to keep your secures locked down tight, and not running WP-CLI PHP as root.

 

 

### Note on --ssh

When dealing with the --ssh parameter in WP CLI it is best to use pure WP CLI. GP CLI will not accommodate this parameter. Continue below for details.

## How to Use Regular WP-CLI on GridPane

To use regular WP-CLI on your GridPane servers there are 2 things you need to know/do:

Below are the recommended steps.

### Step 1. Navigate to your websites directory

To make sure we’re in the right place, we’ll start my navigating to the websites /htdocs directory with the following (replace site.url with your website URL):

```
cd /var/www/site.url/htdocs
```

### Step 2. Choose How You Want to Run Your Commands

You have 2 options for running your commands via the website system user. The first is to simply specify it as a part of the command, and may be the easier option if you’re just running a single command. Here’s an example:

```
sudo -u mysystemuser wp {command} {arg}
```

The second option is to swap over to your websites system user (make sure you use your websites actual system user):

```
su mywebsiteuser
```

And from here you can run your commands as normal. On the command line it will then look a little different to running as the root user:

```
root@myserver:/var/www/test2.com/htdocs# su testTEST38testTEST38@myserver:/var/www/test2.com/htdocs$
```

### Step 3. Run your WP-CLI commands

We’re now in the right directory and you’re ready to go ahead and run your WP-CLI commands.

Once complete, if you swapped into your sites system user, you can return to the root user by typing:

```
exit
```

 

## Further Reading

If you’re looking for some useful WP-CLI commands (or other generally useful commands), these articles may also be of interest:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

