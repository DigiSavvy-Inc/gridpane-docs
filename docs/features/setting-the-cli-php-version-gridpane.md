# Setting the CLI PHP Version | GridPane

# Setting the CLI PHP Version

 

3 min read 

## Introduction

Out of the box, our default CLI PHP version is set to PHP 7.4. In the near future, this will be updated to be 8.0 out of the box.

This change will take place automatically, and so will future updates. For most GridPane users, you can leave our defaults and stop reading right now.

For a few of you though, you may come across a situation where you need to change our defaults to a higher or lower version of PHP, and this article will walk you through how to make this change and set it so that our systems don’t automatically update it in the future.

### Table of Contents

 

## CLI PHP vs Website PHP

Before we begin, it’s important to understand the CLI PHP version, and the version of PHP that your individual websites run on is not the same thing. Updating your website’s PHP version will not solve any issues that arise from scripts/software that does not support your current CLI version of PHP.

### What is PHP CLI?

PHP CLI is PHP’s Command Line Interface, and it allows PHP to be executed from the server command line.

### A Real World Example: Composer

Most programs have a minimum PHP requirement. Back in the days when 7.2 was our default CLI PHP version, Composer made an update that required a minimum of PHP 7.3.

This caused problems not just with Composer but other programs as well – here’s an example of an error from a site where SSO was failing to generate a login link:

```
Your Composer dependencies require a PHP version ">= 7.3.0". You are running 7.2.25-1+ubuntu18.04.1+deb.sury.org+1. Error Code: 100 | PHP Errors stopping SSO Link creation, please check logs....
```

Here Composer is using the CLI PHP version and not the FPM/LSPHP version that is used by your websites. Switching the website PHP version of your sites would, therefore, not fix this issue.

Updating the CLI PHP version to 7.3 fixed the above SSO errors and allowed Composer to once again function correctly.

 

## Getting Started

To make this change, you will first need to SSH into your server. Once connected, the rest is simply a copy-and-paste exercise following our steps below.

Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Checking Your CLI PHP Version

To check your CLI PHP version, you can run the following command:

```
sudo update-alternatives --display php
```

This will output the following, only with the correct PHP version should your setting be different:

```
root@servername:~# sudo update-alternatives --display phpphp - manual modelink best version is /usr/bin/php8.1link currently points to /usr/bin/php7.4link php is /usr/bin/phpslave php.1.gz is /usr/share/man/man1/php.1.gz/usr/bin/php7.3 - priority 73slave php.1.gz: /usr/share/man/man1/php7.3.1.gz/usr/bin/php7.4 - priority 74slave php.1.gz: /usr/share/man/man1/php7.4.1.gz/usr/bin/php8.0 - priority 80slave php.1.gz: /usr/share/man/man1/php8.0.1.gz/usr/bin/php8.1 - priority 81slave php.1.gz: /usr/share/man/man1/php8.1.1.gzroot@servername:~#
```

 

## Changing Your CLI PHP Version on Nginx or OpenLiteSpeed

 

 

### Nginx and OpenLiteSpeed Update

As of November 8th 2022, setting the PHP CLI version on both Nginx and OpenLiteSpeed has been brought to parity so that the same commands work on both server stacks.

### Step 1. Set Your Preferred CLI PHP Version

Run the following command to change the PHP CLI version:

```
sudo update-alternatives --set php /usr/bin/phpX.X
```

X.X = the version number, for example: 7.4, 8.0, 8.1.

For example:

```
sudo update-alternatives --set php /usr/bin/php7.4
```

### Step 2. Make the Change Persist

Our systems check for a token file for the CLI PHP version. If it’s not present, your changes will be reverted. Create the token file with:

```
/root/preferred_php_cli.version
```

Add the PHP version – number only. For example:

```
7.4
```

Now save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

