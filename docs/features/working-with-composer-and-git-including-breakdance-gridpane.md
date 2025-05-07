# Working With Composer and Git (Including Breakdance) | GridPane

# Working With Composer and Git (Including Breakdance)

 

4 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

### Table of Contents

 

## Introduction

If you’re using a theme or plugin that requires Composer, it will likely result in a fatal error on activation. The popular Breakdance builder plugin uses Composer, and this article will walk you through how to use Composer with our Git integration using Breakdance as an example. The script provider can be adjusted to work with any plugin that requires Composer to function.

### The Fatal Error

This following fatal error example is because when Breakdance is deployed via Git, you will need to use composer via the deploy scripts to install its dependencies. It looks as follows:

 

```
This is the error that it is showing: Fatal error: Uncaught Error: Class 'Breakdance\Lib\Vendor\Whoops\Handler\Handler' not found in /var/www/example.com/htdocs/wp-content/plugins/breakdance/plugin/error-reporter/error-reporter-ajax-handler.php:12 Stack trace: 
#0 /var/www/example.com/htdocs/wp-content/plugins/breakdance/plugin/error-reporter/base.php(5): require_once() 
#1 /var/www/example.com/htdocs/wp-content/plugins/breakdance/plugin/base.php(7): require_once('/var/www/exampl...') 
#2 /var/www/example.com/htdocs/wp-content/plugins/breakdance/plugin.php(36): require_once('/var/www/exampl...') 
#3 /var/www/example.com/htdocs/wp-settings.php(447): include_once('/var/www/exampl...') 
#4 /var/www/example.com/wp-config.php(140): require_once('/var/www/exampl...') 
#5 /var/www/example.com/htdocs/wp-load.php(55): require_once('/var/www/exampl...') 
#6 /var/www/example.com/htdocs/wp-blog-header.php(13): require_once('/var/www/exampl...') 
#7 /var/www/example.com/htdocs/index.php(17): require('/var/www in /var/www/example.com/htdocs/wp-content/plugins/breakdance/plugin/error-reporter/error-reporter-ajax-handler.php on line 12
```

## Predeploy Script

Our Git integration offers multiple deployment scripts that can be run before or after deploying your Git repositories. There are two predeploy scripts  and two postdeploy scripts, and these can can be added to the gpconfig directory inside your repo like so:

These are bash scripts, and we’ll be using the predeploy-server.sh. This will run prior to the Git pull. More information on all of these scripts can be found here:

An Overview of GridPane Git Options: Full and Hybrid Repo Types

 

 

### Information

This will work on both regular Git websites and multitenancy Git websites.

### Breakdance Predeploy-server Script

Add the following to your predeploy-server.sh:

 

```
#!/bin/bash
timeout 300 wget https://getcomposer.org/download/2.5.4/composer.phar
timeout 300 chmod 755 $GP_GIT_RELEASE_PATH/wp-content/plugins/breakdance/plugin/vendor/bin/mozart
export COMPOSER_ALLOW_SUPERUSER=1
timeout 300 php composer.phar update -n --working-dir=$GP_GIT_RELEASE_PATH/wp-content/plugins/breakdance/plugin/
timeout 300 php composer.phar install -n --working-dir=$GP_GIT_RELEASE_PATH/wp-content/plugins/breakdance/plugin/
```

Push the changes, and Breakdance should now activate and operate as expected.

 

## Troubleshooting

If you receive a shellcheck error after deploying your repo with the above script present, this will be due to a formatting issue.

Error: /var/www/breakdance.test/releases/release-1678189338/.gpconfig/predeploy-server.sh failed a shellcheck

### Running a Shellcheck

To confirm the reason for the shellcheck error, you can copy the given path and run the following:

```
shellcheck --exclude="SC2145,SC2068,SC2261,SC2086,SC2034" "/path/to/predeploy-server.sh"
```

For example:

```
shellcheck --exclude="SC2145,SC2068,SC2261,SC2086,SC2034" "/var/www/breakdance.test/releases/release-1678189338/.gpconfig/predeploy-server.sh"
```

You’ll likely see the following:

```
^-- SC1017: Literal carriage return. Run script through tr -d '\r' .
```

### The Fix

To fix the issue do the following:

This should remove any unexpected formatting that’s causing the shellcheck failure.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

