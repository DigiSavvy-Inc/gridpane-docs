# Useful WP-CLI Commands for Managing WordPress Websites | GridPane

# Useful WP-CLI Commands for Managing WordPress Websites

 

11 min read 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='673'%20viewBox='0%200%201024%20673'%3E%3C/svg%3E)

## Introduction

WP-CLI is the command line interface for WordPress and is a fantastic tool for helping to manage the websites that you host.

As implied, this is a tool that you use from the terminal, so you will need to connect to your servers in order to use it. This article assumes that you’re already  familiar with how to connect to your server to run a WP-CLI command, but if you need a getting started guide, we have this handy article on two different ways to use WP-CLI on your GridPane servers:

How to Use GP WP-CLI and Regular WP-CLI on GridPane Servers

Along with each command, there’s also a link to the official documentation for easy reference. Let’s get started!

 

 

### Information

In the commands below we use the placeholder "site.url". Be sure to replace this with your target website URL, for example: gridpane.com.

### Quick Reference

WP Core

WP Plugins

WP DB (Database)

WP Search-Replace

WP Users

WP Site

WP Post

Magic Login Link

WP-CLI Help

 

WP Core

 

## Check WordPress Core Integrity

You can use the verify-checksums command to check that your website core files aren’t missing, corrupted, or customized in some way by a previous host or developer. An edited or missing or misplaced file can cause 500 errors.

This will check your core WordPress installation files and let you know if any issues need to be addressed. If there are, see this command.

### GP WP-CLI

```
gp wp site.url core verify-checksums
```

For example:

```
gp wp yourwebsite.com core verify-checksums
```

### WP-CLI

```
wp core verify-checksums
```

 

 

Official Documentation →

## Reinstall WordPress Core

If ever required, you can reinstall WordPress core using WP-CLI. The following command will download the most recent WordPress core without the default themes and plugins (and it won’t overwrite or remove existing themes or plugins.

The [--skip-content] downloads WordPress without the default themes and plugins, and [--force] overwrites existing core files, if they exist.

### GP WP-CLI

```
gp wp site.url core download --skip-content --force
```

### WP-CLI

```
wp core download --skip-content --force
```

 

 

Official Documentation →

WP Plugins

 

## List Your Plugins

If you ever need to quickly view a list of installed plugins for a specific website, this command can be extremely handy. We ourselves use it regularly when reviewing websites for our 360 support service.

### GP WP-CLI

```
gp wp site.url plugin list
```

### WP-CLI

```
wp plugin list
```

### Additional Flags

If you want to see only a list of all active plugins which have updates available, you can use the following GP WP-CLI:

```
gp wp site.url plugin list --field=name --status=active --update=available
```

Or regular WP-CLI:

```
wp plugin list --field=name --status=active --update=available
```

 

 

Official Documentation →

WP DB (Database)

 

 

### Important

Before running any commands that make changes to your WordPress database, please be sure that you take a backup beforehand. This can be done by exporting your database using the WP-CLI below or through the GridPane backups system. Testing on staging first is also a good idea and recommended.

## Export a WordPress Database

Being able to quickly export/create a manual backup of a WordPress database can come in handy when you’re about to perform any kind of clean up (better tested on staging first) or repair.

### GP WP-CLI

```
gp wp site.url db export /var/www/site.url/htdocs/name_of_backup.sql --all-tablespaces --add-drop-table
```

### WP-CLI

```
wp db export name_of_backup.sql --all-tablespaces --add-drop-table
```

You can also check out this article for more database backup options: How to Backup / Export / Import a WordPress Database.

 

 

Official Documentation →

## Import a WordPress Database

Importing a backup through WP-CLI is extremely useful when migrating websites manually or importing a manual backup.

### GP WP-CLI

```
gp wp site.url db import /var/www/site.url/htdocs/name_of_backup.sql
```

### WP-CLI

```
wp db import name_of_backup.sql
```

 

 

Official Documentation →

## Check the Health of a WordPress Database

If you’re seeing performance issues or database errors, then checking your database for corrupted data is a necessary troubleshooting check. You can check the health of a website’s database as follows:

### GP WP-CLI

```
gp wp site.url db check
```

### WP-CLI

```
wp db check
```

If you see any issues, see the repair commands below.

 

 

Official Documentation →

## Repair a WordPress Database

If necessary, you can use this command to repair a corrupted database. Always back up your database before performing work on it.

### GP WP-CLI

```
gp wp site.url db repair
```

### WP-CLI

```
wp db repair
```

 

 

Official Documentation →

## Optimize Your Database

This WP-CLI command can optimize your WordPress tables for better efficiency.

### GP WP-CLI

```
gp wp site.url db optimize
```

### WP-CLI

```
wp db optimize
```

 

 

Official Documentation →

WP Search-Replace

 

## Search and Replace in a WordPress Database

### Test With a Dry Run Using GP WP-CLI

Before running your search and replace, we recommend doing a dry run first. You can do this with:

```
gp wp site.url  search-replace '{old URL}' '{new URL}' --dry-run --skip-columns=guid
```

For example:

```
gp wp site.url search-replace 'oldwebsite.com' 'newwebsite.com' --dry-run --skip-columns=guid
```

### WP-CLI Example:

```
wp search-replace 'oldwebsite.com' 'newwebsite.com' --dry-run --skip-columns=guid
```

You will be shown a table detailing the replacements that would be made:

Followed by a notice will the total number of replacements: Success: 'X' replacements to be made.

### Search and Replace with GP WP-CLI

We can now run our search and replace as follows:

```
gp wp site.url search-replace '{old URL}' '{new URL}' --precise --recurse-objects --all-tables
```

For example:

```
gp wp site.url search-replace 'http://oldwebsite.com' 'https://newwebsite.com' --precise --recurse-objects --all-tables
```

### WP-CLI Example

```
wp search-replace 'http://oldwebsite.com' 'https://newwebsite.com' --precise --recurse-objects --all-tables
```

 

 

Official Documentation →

WP USERS

 

## List the Users of a Website

If you’d like to display a list of users for a specific website, you can easily do so with WP-CLI. You can also specify users by role type.

### GP WP-CLI

```
gp wp site.url user list gp wp site.url user list wp user list --role=administrator
```

### WP-CLI

```
wp user list
wp user list --role=administrator
```

The default role types are:

The list displayed will include a corresponding user ID at the very beginning. This is necessary for some of the commands detailed below. Here’s an example:

```
+----+-------------+--------------+--------------------+---------------------+-----------+| ID | user_login  | display_name | user_email     | user_registered     | roles         |+----+-------------+--------------+--------------------+---------------------+-----------+| 1  | my-user     | My Name      | [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection) | 2023-02-06 08:45:07 | administrator |+----+-------------+--------------+--------------------+---------------------+-----------+
```

 

 

Official Documentation →

## Create a New WordPress User

When you don’t have admin access to a website, the easiest way to create a new user is through WP-CLI – far easier than manually adding one through PHPMyAdmin. Below is how to create a new administrator account, but you can switch out administrator for any role type, and of course, be sure to switch out the username and email address.

### GP WP-CLI Example

```
gp wp site.url user create username [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection) --role=administrator
```

### WP-CLI Example

```
wp user create username [[email protected]](https://gridpane.com/cdn-cgi/l/email-protection) --role=administrator
```

 

 

Official Documentation →

## Reset the Password For a WordPress User

As with the command above, if you don’t have access to a website then WP-CLI is an easy way to reset the password for a user.

Before you begin you’ll need the WordPress users ID – see how to display a list of users here. The number at the end is the user ID, and this command will send a password reset email.

### GP WP-CLI

```
gp wp site.url user reset-password 1
```

### WP-CLI

```
wp user reset-password 1
```

### Alternative Reset

The commands below allow you to update a user and specify the exact password:

```
gp wp site.url user update 1 --user_pass=pO11HDehwfn6v63I6qwdYvdHj
```

```
wp user update 1 --user_pass=pO11HDehwfn6v63I6qwdYvdHj
```

 

 

Official Documentation →

## Change the Admin Email Address for a WordPress User

Without admin access, changing an admin email address is easiest done via WP-CLI. Before you begin, you’ll need the WordPress users ID – see how to display a list of users here.

Replace the email address in the commands below with the new user’s email address.

### GP WP-CLI

```
gp wp site.url user update 1 --user_email=[[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

### WP-CLI

```
wp user update 1 --user_email=[[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)
```

You can confirm your change was successful with the wp user list command.

 

 

Official Documentation →

## Modify a WordPress User Role

Without admin access, changing a WordPress user’s role is easiest done via WP-CLI. Before you begin, you’ll need the WordPress users ID – see how to display a list of users here.

In the following example, it sets the role as administrator, but be sure to set the correct role for your use case.

### GP WP-CLI

```
gp wp site.url user set-role 1 administrator
```

### WP-CLI

```
wp user set-role 1 administrator
```

You can confirm your change was successful with the wp user list command.

 

 

Official Documentation →

WP Site

 

## Remove Website Content

This handy WP-CLI command can be used to completely remove ALL content from a website.

One use case for this is installing demo content from a theme to speed up your workflow. Typically those processes add a bunch of content that’s not needed, including published pages, posts, comments, etc. This command can remove all of this without touching any of your settings.

### GP WP-CLI

```
gp wp site.url site empty
```

### WP-CLI

```
wp site empty
```

### Bonus: Remove Website Uploads

As with the above use case, you can also use the following flag to remove all contents from your uploads folder:

```
gp wp site.url site empty --uploads
```

Or:

```
wp site empty --uploads
```

 

 

Official Documentation →

WP Post

 

## Generate Dummy Content for Testing

If you’re a developer in need of content for testing purposes, this CLI could come in very handy. The command creates 20 empty posts, but you can create significantly more if needed.

In my testing, generating 200 posts with lorum ipsum content took 3 seconds.

### GP WP-CLI

```
gp wp site.url post generate --count=20
```

### WP-CLI

```
wp post generate --count=20
```

### Add Some Ipsum…

The above generates empty posts, but if you’d like to add some text to these, you can do so following these pirate ipsum examples – GP WP-CLI:

```
echo -e "Pink broadside jack cable fore Pirate Round reef scourge of the seven seas me Corsair. Keelhaul killick swab reef heave down avast topmast Buccaneer fore rutters. Salmagundi fathom come about overhaul run a shot across the bow dance the hempen jig snow yard Nelsons folly six pounders.\n\nGrapple aft brig pressgang jolly boat pink swing the lead tender mizzen rutters. Barkadeer rope's end scuttle parrel boatswain Blimey starboard bilge Brethren of the Coast scourge of the seven seas. Nipper scurvy grog belay Chain Shot hornswaggle stern chase dance the hempen jig Buccaneer." | gp wp site.url post generate --count=20 --post_content
```

Or WP-CLI:

```
echo -e "Pink broadside jack cable fore Pirate Round reef scourge of the seven seas me Corsair. Keelhaul killick swab reef heave down avast topmast Buccaneer fore rutters. Salmagundi fathom come about overhaul run a shot across the bow dance the hempen jig snow yard Nelsons folly six pounders.\n\nGrapple aft brig pressgang jolly boat pink swing the lead tender mizzen rutters. Barkadeer rope's end scuttle parrel boatswain Blimey starboard bilge Brethren of the Coast scourge of the seven seas. Nipper scurvy grog belay Chain Shot hornswaggle stern chase dance the hempen jig Buccaneer." | wp post generate --post_content --count=20
```

Some lorum ipsum generators, such as Bacon Ipsum (WP-CLI tutorial), have an API that allows you to generate paragraphs of text, which, in theory, could be used via curl. In my testing, I ran into an error that prevented the regular method from working, but you can learn more details here and in the link above.

 

 

Official Documentation →

Magic Login Link

 

## Create a Magic Login Link

You can quickly and easily create a magic login link to login to any of your websites directly on your server. Normally, you can just SSO in from inside your GridPane account, but if for some reason that’s not working, or you need to send a login link to a client (not really recommended), you can create one as outlined below.

Note: Links expire after 15 minutes or once they’ve been successfully used.

### GP WP-CLI

```
gp wp site.url login create 1
```

### WP-CLI

```
wp login create 1
```

Note: This is not a WP-CLI  core command, so there’s no official documentation link.

 

Help Commands

 

## WP-CLI Help Command

WP-CLI has its own built-in help reference that you can use to learn more about a specific WP-CLI command and its available functions. This includes a synopsis, parameters, available fields, options, and some examples.

The standard help command syntax is as follows:

```
wp help {wp-cli-command}
```

### GP WP-CLI Example

```
gp wp site.url help plugin list
```

### WP-CLI Example

```
wp help plugin list
```

 

 

Official Documentation →

More CLI!

 

## Further Reading

If you would like to learn more about WP-CLI and the other available core commands, you can view the official full documentation at WordPress.org:WordPress Developer Tools: WP-CLI

Many plugins also have their own WP-CLI that can also be used the same way. This can usually be found in their own documentation if available.

For other useful commands, these articles may also be of interest:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

