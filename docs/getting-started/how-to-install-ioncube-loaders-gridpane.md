# How to Install Ioncube Loaders | GridPane

# How to Install Ioncube Loaders

 

4 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

## Introduction

While quite rare, you might find that one of your plugins (or other software) is encrypted with IonCube, and in order for them to work correctly, you might need to install the IonCube loaders into PHP on your server.

Warning: Ioncube is third-party software and isn’t supported by GridPane. Additionally, if it breaks the server, the server won’t be supported. That being said, this is pretty safe.

### Table of Contents

 

## IonCube, PHP 8.0, and GridPane

IonCube has chosen to skip adding support for PHP 8.0 and instead go straight from 7.4 to supporting PHP 8.1 (Source).

However, GridPane now uses PHP 8.0 for the CLI PHP version, which means our default setting is not compatible with IonCube loaders.

### How to Use IonCube at GridPane

As PHP 8.0 is not supported, this means you need to use either PHP 7.4 or PHP 8.1. To do so, you’ll need to change your CLI PHP version on your server.

This is a simple task, and we have the following article that will walk you through the process for both Nginx and OpenLiteSpeed:

Setting the CLI PHP Version

 

## Getting Started

Before you get started, make sure you’ve generated an SSH key and have successfully logged into your server as root. The following guides detail how to do this:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Install On Nginx

### Step 1: Download the Ioncube loaders

```
wget http://downloads3.ioncube.com/loader_downloads/ioncube_loaders_lin_x86-64.tar.gz
```

### Step 2: Extract the Ioncube loaders

```
tar xzf ioncube_loaders_lin_x86-64.tar.gz -C /usr/local
```

### Step 3: Load it

Right now, the current PHP CLI version is 8.0 which is not supported. You will need choose either PHP 7.4 or PHP 8.1.

For PHP 7.4 you can run the following:

```
echo 'zend_extension = /usr/local/ioncube/ioncube_loader_lin_7.4.so' | tee -a /etc/php/7.4/cli/php.ini && echo 'zend_extension = /usr/local/ioncube/ioncube_loader_lin_7.4.so' | tee -a /etc/php/7.4/fpm/php.ini && gp php 7.4 restart
```

For PHP 8.1 you can run:

```
echo 'zend_extension = /usr/local/ioncube/ioncube_loader_lin_8.1.so' | tee -a /etc/php/8.1/cli/php.ini && echo 'zend_extension = /usr/local/ioncube/ioncube_loader_lin_8.1.so' | tee -a /etc/php/8.1/fpm/php.ini && gp php 8.1 restart
```

### Step 4. Confirm it’s working

Run the following:

```
php -v
```

Assuming you’ve already changed your CLI PHP version as mentioned above, the output should include IonCube like as follows:

```
PHP 7.4.32 (cli) (built: Sep 29 2022 22:24:52) ( NTS )Copyright (c) The PHP GroupZend Engine v3.4.0, Copyright (c) Zend Technologieswith the ionCube PHP Loader + ionCube24 v12.0.2, Copyright (c) 2002-2022, by ionCube Ltd.with Zend OPcache v7.4.32, Copyright (c), by Zend Technologies
```

You’re done!

 

## Install On OpenLiteSpeed

### Step 1: Install the required version

Run the following command to install IonCube module for the PHP version you want.

```
apt install lsphp74-ioncube
```

You can replace 74 with 81 for PHP 8.1.

### Step 2. Confirm it’s working

Run the following command ( with the respective PHP version )

```
/usr/local/lsws/lsphp74/php -v
```

Or you can run the following for the default server PHP version

```
php -v
```

The output should include IonCube like as follows:

```
PHP 7.4.28 (cli) (built: Mar 15 2022 04:25:07) ( NTS )Copyright (c) The PHP GroupZend Engine v3.4.0, Copyright (c) Zend Technologieswith the ionCube PHP Loader + ionCube24 v10.4.1, Copyright (c) 2002-2020, by ionCube Ltd.with Zend OPcache v7.4.28, Copyright (c), by Zend Technologies
```

You’re done!

### LiteSpeed Ioncube Documentation

LiteSpeed’s own documentation (including a manual alternative) can be found here: PHP Extensions: Install IonCube Loaders on LiteSpeed/OpenLiteSpeed

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

