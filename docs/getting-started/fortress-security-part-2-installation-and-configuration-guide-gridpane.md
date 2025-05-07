# Fortress Security Part 2: Installation and Configuration Guide | GridPane

# Fortress Security Part 2: Installation and Configuration Guide

 

27 min read 

### Table of Contents

Advanced Configuration with WP-CLI
Logs and Further Reading
 

## Introduction

This article will walk you through how configuring the Fortress security plugin works, and the main settings that we believe you may wish to configure websites when the baseline configuration doesn’t meet your needs.

This article covers how to configure Fortress via your GridPane dashboard and/or WP-CLI. For information on working with the Fortress JSON, this information has been moved to its own article here: Fortress Part 4. JSON Configs & Creating a Server-Level Configuration

 

 

### Fortress Developer Documentation

For all other settings that are not covered, the official Developer Documentation for Fortress can be found here:

Official Fortress Developer Documentation

Customizing Fortress settings may seem complicated at first glance, but configuring the different modules is relatively straightforward, and multiple sites can share the same configuration. Once you understand the basic setup, you’ll have a tremendous amount of flexibility for configuring Fortress across all of your websites.

 

### GridPane’s Auto-Configuration

For a smooth integration into GridPane, our Fortress install auto-configures necessary firewall and caching exclusions and sets up a consistent config directory that works with our cloning and staging systems. This includes:

 

Part 1: Quickstart Onboarding

 

## Getting Started: Recommended Steps

Onboarding is now a few clicks via the UI, which you can find by opening your website customizer and navigating through to the Security tab:

The commands in the “Run Fortress Command” dropdown are already ordered in the recommended order for you to run them, and here are the recommended steps you should take for each website:

You can safely run step 6 even if you’re not sure if everything else is set up. If one or more Administrator users have not set up 2FA for their account, the command will error and write to the log output.

That’s all there is to it! You can find further details below on activating Fortress and setting up 2FA.

 

 

### Important: MyISAM Warning

Fortress will not work with the MyISAM storage engine (for MySQL databases). This storage engine is slow and outdated, and often a primary cause for unusual slow behavior in a website. To use Fortress, you will need to update any MyISAM database tables to use the InnoDB storage engine.

You can learn how to check for MyISAM tables and how to convert MyISAM to InnoDB in this article:
Converting MyISAM to InnoDB

## Install and Uninstall Fortress

Fortress can be installed and uninstalled directly within your GridPane account. Once our billing component is completed, this will be available for all plans.

To get started, head over to the Sites page inside your GridPane account and click on the name of the site you want to configure Fortress on to open up the website customizer.

Note: We recommend taking a backup before you proceed.

Next, click through to the Security tab, and here you will see the option to toggle Fortress ON and OFF:

### Fortress Installation

GridPane installs Fortress as a must-use plugin. This is necessary to ensure that malicious code can’t simply deactivate it—a major flaw in installing any security plugin as a regular plugin.

 

## Setting Two-Factor Authentication for Your Own Account

Once Fortress has been installed, the only thing necessary to do is set up two-factor authentication for your account and any other administrators and/or editors.

### Setting up 2FA

After a user whose role mandates TOTP-2FA logs in (administrator and editor by default), they will be intercepted and redirected to the TOTP setup page:

You can skip it initially, but only once.

After clicking the “Setup two-factor authentication” button, Fortress will generate and persist a new set of TOTP credentials for the user.

Scan the displayed QR code or copy the revealed secret.

To prevent account lockout due to a mismatch between Fortress and the authenticator app, Fortress will not activate TOTP-2FA until the user provides a valid OTP.

Once set, the next time you log in, you will be required to enter your 2FA authentication code or recovery code:

You can read the full TOTP developer documentation here.

 

Part 2: Configuring Fortress Overview

 

## Configuring Fortress

With the exception of setting up 2FA, which is done inside of your WordPress admin, there are two ways that Fortress can be configured:

A selection of the most commonly used Fortress WP-CLI can also be run directly from your GridPane dashboard via the website customizer > Fortress tab:

### WP-CLI via GPFort CLI

Fortress is built with a CLI-first approach to allow maximum automation in your workflow. Full developer documentation can be found here.

At GridPane, we have our custom gpfort CLI, which, similar to GP WP-CLI, allows you to run Fortress WP-CLI commands as the root user (more details in this section below).

### Fortress Configuration JSON Files

Fortress has 3 JSON files which are used to configure the majority of settings, including custom settings such as encrypting sensitive information such as Stripe API keys. These are:

###### Baseline (default) configuration

The baseline configuration is what Fortress ships out of the box and has been designed to work for 95% of all use cases (meaning most brochure websites). To view the most up-to-date Fortress baseline configuration, please check the official developer documentation here: Fortress Baseline Configuration

###### Server level configuration

The server-config.json can be used to customize your own settings and apply them to ALL websites on a server. These settings override the baseline configuration.

###### Website level configuration

The config.json is the site-level config file. This can be configured on a per-site basis, and any settings here will override the settings in the baseline and server-config.json files.

The complete configuration reference can be found here.

 

## GPFort CLI and Fortress WP-CLI

As a part of our integration with Fortress, we’ve created our gpfort CLI and this is our recommended way to run Fortress’s WP-CLI.

When running Fortress WP-CLI via gpfort:

### GPFort Syntax

gpfort follows a similar syntax to our GP-CLI but requires an extra flag that needs passing after the site.url. Here’s the syntax for individual websites:

```
gpfort {site.url} -cli {wp-cli-command} {args}
```

The following is the syntax for all sites on a server:

```
gpfort all-sites -cli {wp-cli-command} {args}
```

For example:

```
gpfort examplesite.com -cli fort config cache ls
```

```
gpfort all-sites -cli fort config cache ls
```

 

## GridPane Fortress Configuration Files

GridPane includes a server-config.json file, which allows you to set custom Fortress settings for all websites on a server. The site-specific config.json which can be used for customizing individual sites. These are located as follows:

```
/etc/fortress/server-config.json
```

```
/var/www/site.url/fortress/config.json
```

Fortress’s inbuilt WP-CLI will directly edit and update the site level config.json.

To set up the server-config.json for one or more of your servers, you will need to edit this file directly. Please see our Fortress part 4 article for details:

Fortress Part 4. JSON Configs & Creating a Server-Level Configuration

 

## View Fortress Configuration Sources

Fortress offers CLI commands that can be used to view all your configuration sources as JSON.

### View Configuration Sources

You can now run this command inside your GridPane account via the website customizer > Security tab: Details here.

This CLI command also allows you to view the current configuration sources (replace site.url with your website URL):

```
gpfort site.url -cli fort config ls
```

Full developer documentation here.

### View Cached Configuration

You can now run this command inside your GridPane account via the website customizer > Security tab: Details here.

The following CLI command can also be used to display the currently cached configuration as JSON (replace site.url with your website URL):

```
gpfort site.url -cli fort config cache ls
```

Full developer documentation here.

 

Part 3: Configuring 2FA

 

## Two-Factor Authentication

By default, Fortress treats Administrator and Editor user roles as privileged users. Depending on your use case, you may wish to change these defaults and potentially add in other roles, such as shop_manager on WooCommerce stores. The following sections will look at how to make these changes and also how to enforce the requirement to successfully pass 2FA verification in order to be able to log in.

 

### Adjusting Privileged User Roles

Here’s an example of how to make the role “shop_manager” a privileged user inside of Fortress.

This can be done in either the site configuration file or the server configuration file but would be better enabled only when needed, and thus in the site configuration.

You can add the following setting to your site configuration file along with the default roles with the following WP-CLI command (replace site.url and your desired user role):

```
gpfort site.url -cli fort config update auth.require_2fa_for_roles='["administrator","editor","shop_manager"]'
```

For example:

```
gpfort yourwebsite.com -cli fort config update auth.require_2fa_for_roles='["administrator","editor","shop_manager"]'
```

###### Additional Notes

 

### Forcing 2FA for Privileged Users

Once all of your website’s privileged users have 2FA configured, you can now enforce that each user must have TOTP-2FA configured BEFORE they are allowed to log in.

This can be enforced by adding your websites privileged_user_roles to the require_2fa_for_roles_before_login setting inside the configuration file.

###### Protection

Forcing 2FA will protect your website against the following attack vectors:

Once configured, any privileged user without TOTP-2FA configured will see the following message when they attempt to log in:

###### JSON Settings

Only do this AFTER all of your website’s privileged users have 2FA configured for their accounts.

It’s best to set this inside the website configuration file instead of the server configuration, as it will make adding Fortress to new sites easier.

You can adjust the following and your settings to your site configuration file (replace site.url with your website URL):

```
gpfort site.url -cli fort config update auth.require_2fa_for_roles_before_login='["administrator","editor"]'
```

###### Additional Notes

 

Part 4: Configuring the Password Module

 

## Password Configuration

If you need to:

You can find the necessary details below. For all other settings, please refer to the official developer documentation here.

 

 

### Information

Fortress's password module will hash new passwords using Fortress's secure hashing. If you deactivate Fortress, any passwords that have been secured with upgraded cryptography will need to be reset.

### Upgrade Existing Passwords to Secure Password Hashing

You can now run this command inside your GridPane account via the website customizer > Security tab: Details here.

The following WP-CLI command can be used to upgrade all password hashes of existing users to Fortress’s secure password hashing:

```
gpfort site.url -cli password upgrade-legacy-hashes
```

You will be asked to confirm. Type yes or no and then press Enter.

###### Additional Notes

 

### Password resets for privileged users

Password resets are disabled for privileged users by default. This applies to users of the roles:

The following WP-CLI command can be used to set a new, randomly generated, and secure password for a user.

The command will output the plaintext password so you can copy it to a password manager.

```
wp snicco/fortress password reset {user_name}
```

Here’s the GPFort version:

```
gpfort site.url -cli password reset {user_name}
```

For example:

```
gpfort site.url -cli password reset john-smith
```

###### Additional Notes

 

### Enable or disable application passwords

You can enable or disable application passwords by setting the disable_application_passwords option to true or false.

You can force disable with the following (replace site.url with your website URL):

```
gpfort site.url -cli fort config update password.disable_application_passwords=true
```

Or force enable with:

```
gpfort site.url -cli fort config update password.disable_application_passwords=false
```

###### Additional Notes

 

### Disallow Legacy Password Hashes

You can add additional security to your website by setting the allow_legacy_hashes option to false.

This will prevent one of the most common WordPress hacks where an attacker will add a new user to your website using a password with the default and outdated md5 hashing and then logging in with their newly created credentials.

Fortress allows you to completely prevent this from happening by changing this setting to false.

###### Caution!

Only set allow_legacy_hashes to false if one or more of the following is true for your website:

If one or more of the above isn’t true, you might prevent yourself and other users from being able to log in.

You can disallow legacy hashes with the following WP-CLI command (replace site.url with your website URL):

```
gpfort site.url -cli fort config update password.allow_legacy_hashes=false
```

###### Additional Notes

 

Part 5: Configuring Sessions

 

## Secure Sessions Configuration

If you need to increase sudo mode session timeouts or idle session timeouts, you can find the necessary details below. For all other settings, please refer to the official developer documentation here.

 

### Increasing/Decreasing Sudo Mode Timeout Periods

The sudo_mode_timeout option is the interval in seconds during which Fortress will consider a session to be in sudo mode after logging in.

You can increase or decrease sude timeouts with the following WP-CLI command (replace site.url with your website URL and XXX with your desired time):

```
gpfort site.url -cli fort config update session.sudo_mode_timeout=XXX
```

For example:

```
gpfort mysite.com -cli fort config update session.sudo_mode_timeout=1000
```

###### Additional Notes

 

### Increasing/Decreasing Idle Timeout Periods

The idle_timeout option is the interval in seconds after which a user without activity is logged out.

You can increase or decrease timeouts with the following WP-CLI command (replace site.url with your website URL and XXX with your desired time):

```
gpfort site.url -cli fort config update session.idle_timeout=XXX
```

For example:

```
gpfort website.com -cli fort config update session.idle_timeout=1200
```

###### Additional Notes

 

Part 6: Configuring Vaults & Pillars

 

## Vaults & Pillars

By default, no Vaults & Pillars are active when Fortress is installed. While some settings apply to the vast majority of WordPress websites, not all of them will, and so these need to be determined on a per-site basis.

Below we’ll look at recommendations for settings that you may wish to implement on the vast majority of your websites, and there are links to Snicco’s walkthroughs on securing Stripe API Keys.

To learn more about Vaults & Pillars, you can learn more on the Snicco blog and official Developer Documentation here:

 

### Vaults & Pillars Video Walkthrough

The following technical rundown is a recording by Paul Stoute, a long-time GridPane client, and Calvin Alkan of Snicco.

 

 

 

### Information

To learn how to implement Vaults & Pillars it is best to view Snicco's official developer documentation in full via the link above. Each section of this documentation is important and should be fully read and understood to ensure you understand both how this functionality works and the implications.

 

### Important

Always add/test new vaults in a staging environment before implementing on a production website. No exceptions.

## Vaults

Fortress Vaults can be used to secure confidential and/or sensitive information such as API keys.

### Running WP-CLI Commands for Vaults & Pillars

As the gp wp <domain> <command> wrapper is not intended for programmatic use, you may need to run regular WP-CLI for Fortress Vaults & Pillars when querying the database. The following 3 steps detail how to run regular WP-CLI via your website’s system user.

###### Step 1. Navigate to Your Website’s Directory

To make sure we’re in the right place, we’ll start by navigating to the websites /htdocs directory with the following (replace site.url with your website URL):

```
cd /var/www/site.url/htdocs
```

###### Step 2. Choose How You Want to Run Your Commands

You have 2 options for running your commands via the website system user. The first is to simply specify it as a part of the command and this maybe the easier option if you’re just running a single command. Here’s an example:

```
sudo -u mysystemuser wp {command} {arg}
```

The second option is to swap over to your website system user (make sure you use your website’s actual system user):

```
su mywebsiteuser
```

And from here, you can run your commands as normal. On the command line, it will then look a little different from running as the root user:

```
root@myserver:/var/www/mywebsite.com/htdocs# su testTEST38
testTEST38@myserver:/var/www/mywebsite.com/htdocs$
```

###### Step 3. Run your WP-CLI commands

We’re now in the right directory, and you’re ready to go ahead and run your WP-CLI commands.

Once complete, if you swapped into your site system user, you can return to the root user by typing:

```
exit
```

 

### Securing Stripe API Keys

Calvin Alkan has written easy-to-follow step-by-step guides for securing Stripe API keys in WooCommerce, Easy Digital Downloads (EDD), and Gravity Forms.

With the overwhelming majority of plugins storing Stripe API keys in plaintext in the database and the seemingly never-ending stream of SQLi vulnerabilities in WordPress Core, themes, and plugins that can expose these credentials, it is vital to take steps to encrypt them.

 

## Pillars

### Recommended Pillar Defaults

Below are our recommended default Pillars for WordPress Core settings/options. Please note that these are not added by default when Fortress is activated and must be activated manually.

These settings can help you make the following settings more secure and protect them from malicious abuse and/or user error:

Below details how to create this configuration.

###### Step 1. Strict Mode Check

Please check and, if necessary, disable Strict Mode. Details here.

###### Step 2. Create Your Configuration

Add the above recommended settings to your configuration, and ensure that your permalink, tag, and category bases are all correct.

###### Step 3. Check and Reload Your Configuration

To ensure that your configuration is valid and set your changes live,  run this WP-CLI command to check the Fortress syntax and clear the cache (replace site.url with your website URL):

```
gpfort site.url -cli fort config test --reload-on-success
```

###### Step 4.  Encrypt All Vaults & Replace Pillars With Placeholders

```
gpfort site.url -cli vnp options:seal-all
```

###### Step 5. Optional: Re-enable Strict Mode

If applicable, now you can re-enable Strict Mode.

###### Additional Notes

 

## Strict Mode in Vaults and Pillars

Strict Mode provides a higher level of security by enforcing stricter checks and validations on the options. When enabled, it introduces the following changes and ensures that the system doesn’t fall back to insecure defaults:

Strict Mode best suits environments where security is paramount, but it should be enabled with caution by first thoroughly testing in a staging environment.

###### Checking if Strict Mode is activated

By default, Strict Mode is NOT active, so it will not be active unless you have explicitly activated it in the past.

You can verify if strict mode is enabled with the following WP-CLI command:

```
gpfort site.url -cli fort config cache ls --key=fortress.vaults_and_pillars.strict_option_vaults_and_pillars
```

The returned value indicates whether the strict mode is active (true) or inactive (false).

###### Enabling Strict Mode

You can enable Strict Mode in your Fortress configuration JSON file by setting the strict_option_vaults_and_pillars attribute to true with the following WP-CLI command:

```
gpfort site.url -cli fort config update vaults_and_pillars.strict_option_vaults_and_pillars=true
```

The default value is false. However, enabling Strict Mode is highly recommended in production environments.

###### Disabling Strict Mode

Deactivating has no adverse effects.You can turn off the Strict Mode by updating the strict_option_vaults_and_pillars option to false in your configuration with the following WP-CLI command:

```
gpfort site.url -cli fort config update vaults_and_pillars.strict_option_vaults_and_pillars=false
```

###### Additional Notes

 

Part 7: Configuring the Code Freeze Module

 

## Code Freeze

We recommend that you take advantage of Code Freeze on all of your websites and this module is active by default on installation. This feature offers an excellent layer of additional security with essentially no downside.

These are the different available options:

### Configuration

Code Freeze is set to "auto" by default. It can be disabled and then reset to default within your website customizer. Further details can be found in the section directly below.

###### Additional Notes

 

Part 8: Running Fortress WP-CLI Commands via the UI

 

 

### Developer Plus Accounts Only

The following are currently only available to Developer Plus accounts, however, these will be made available to everyone in the near future.

## Running Fortress WP-CLI Commands from Your GridPane Account

Fortress includes its own WP-CLI, and the GridPane UI allows you to turn the commands that follow in the sections below directly from your GridPane account.

These specific commands allow you to easily run the most common tasks you may need. Simply choose the command you wish to run from the dropdown and hit the Run button.

### Further Commands and Info

You can view all of the available Fortress WP-CLI commands in the official Developer Documentation here:

Developer Docs: Fortress WP-CLI Integration

And this section details how to run Fortress WP-CLI for your GridPane websites:

GPFort and Fortress WP-CLI

 

### 1. Update password storage to Fortress’s secure hashing

This runs the following command:

```
gpfort site.url -cli fort password upgrade-legacy-hashes --ack=password-hashes-can-currently-not-be-reversed
```

This command can be used to upgrade ALL existing user password hashes to Fortress’s secure password hashing.

 

### 2. Optimize Fortress configuration

This runs the following command:

```
gpfort site.url -cli fort config optimize
```

This command will optimize your website configuration sources depending on the current state of the WordPress site.

This command will only make safe changes, and running it will never break a site’s configuration.

 

### 3. Require 2FA to be configured for admins and editors

This runs the following command:

```
gpfort site.url -cli fort config update auth.require_2fa_for_roles_before_login+=administrator,editor --no-interaction
```

This command requires that users with the WordPress Administrator and Editor roles must use 2FA in order to be able to login. If they have not previously set up 2FA, they will not be able to login. This protects against privilege escalation attacks.

 

### 4. Disable CodeFreeze

This runs the following command:

```
gpfort site.url -cli config update code_freeze.enabled=no
```

This command force disables code freeze, ensuring that it is not active.

 

### 5. Reset CodeFreeze to default

This runs the following command:

```
gpfort site.url -cli config update -code_freeze.enabled
```

This command removes the short-circuit constant if you have previously ran Force Disable Code Freeze option.

 

### 6. (!!!) Allow password resets for all users (!!!)

We do not recommend running this command on ALL websites. This should be used on a case-by-case basis.

This runs the following command:

```
gpfort site.url -cli fort config update password.disable_web_password_reset_for_roles=[]
```

By default, Administrator and Editor users cannot request password resets. This command will allow ALL users to request password resets.

 

### 7. (!!!) Revert password reset config to Fortress defaults (!!!)

This runs the following command:

```
gpfort site.url -cli fort config update -password.disable_web_password_reset_for_roles --ignore-missing-delete
```

This command will remove the password module "disable_web_password_reset_for_roles" configuration from your website config.json.

This will revert #6 above and/or remove any custom changes you have made to other users resetting passwords.

 

### 8. (!!!) Loosen session timeouts (!!!)

We do not recommend running this command on ALL websites. This should be used on a case-by-case basis.

This runs the following command:

```
gpfort site.url -cli fort config update session.idle_timeout=7200 session.sudo_mode_timeout=3600 session.absolute_timeout_remembered_user=172800
```

This command will extend the session timeout period

 

### 9. Re-enable WordPress application passwords

This runs the following command:

```
gpfort site.url -cli fort config update password.disable_application_passwords=false
```

This command re-enables application passwords should you have a website that needs to use them.

 

### 10. Log out all users

This runs the following command:

```
gpfort site.url -cli fort session destroy-all
```

This command will destroy ALL user’s session data in the database. This is a quick and effective way to force all users to log in again.

 

### 11. Seal all configured Vaults&Pillars

This runs the following command:

```
gpfort site.url -cli fort vnp option seal-all --force
```

This command can be used to encrypt all configured Vaults and replace all configured Pillars with placeholders in the database.

 

### 12. Unseal all configured Vaults&Pillars

This runs the following command:

```
gpfort site.url -cli fort vnp option unseal-all --skip-plugins --skip-themes --skip-packages --force
```

This command can be used to decrypt all configured Vaults and replace all configured Pillars placeholders in the database with the actual values.

 

### 13. Test current configuration

This runs the following command:

```
gpfort site.url -cli fort config test --no-interaction
```

This command can validate that your current configuration sources will build a valid configuration cache.

 

### 14. Test current configuration with WordPress Core only

This runs the following command:

```
gpfort site.url -cli fort config test --skip-plugins --skip-themes --skip-packages --no-interaction
```

This command can validate that your current configuration sources will build a valid configuration cache while bypassing themes and plugins when running WP-CLI.

 

### 15. Output custom configuration sources

This runs the following command:

```
gpfort site.url -cli fort config ls
```

This command can be used to display detailed information about the configuration sources that Fortress uses on a site and is particularly useful for troubleshooting.

You can view the output directly inside the UI by clicking the Fortress GP-CLI Log button.

 

### 16. Output currently cached config

This runs the following command:

```
gpfort site.url -cli fort config cache ls
```

Running this command via the UI will output the cached config to the GP-CLI log. You can view the output directly inside the UI by clicking the Fortress GP-CLI Log button.

 

### 17. Output version information

This runs the following command:

```
gpfort site.url -cli fort version
```

This command can be used to display information about the current Fortress installation, such as version and commit hash.

You can view the output directly inside the UI by clicking the Fortress GP-CLI Log button.

 

### 18. [LEGACY] Remove CodeFreeze Short-Circuit constant

This runs the following command:

```
gpfort site.url -cli -remove-codefreeze-shortcircuit
```

This command removes the short-circuit constant if you have previously ran Force Disable Code Freeze option.

 

GridPane UI: Fortress Logs

 

 

### Developer Plus Accounts Only

The following are currently only available to Developer Plus accounts, however, these will be made available to everyone in the near future.

## GridPane UI: Viewing the Fortress Logs

Inside your GridPane account, you can now view the following three logs:

These can be found inside the website customizer in the security tab:

### Fortress Log & Audit Log

These logs detail Fortress events and are useful for troubleshooting purposes.

### Fortress GP-CLI Log

All output from GridPane functionality and running Fortress WP-CLI can be viewed directly inside this log. This includes all of the output from the WP-CLI commands found in the same tab in the “Run Fortress Command” dropdown.

 

Troubleshooting

 

## Troubleshooting: Fortress Part 3

Our troubleshooting info has been moved to its own article. Please see part 3 in our Fortress series for further information:

Fortress Security Part 3: Troubleshooting

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

