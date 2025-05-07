# How to Optimize Database Performance With MySQLTuner | GridPane

# How to Optimize Database Performance With MySQLTuner

 

7 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

 

### Information

MySQLTuner is not necessary for high performance on GridPane, and very few of our users ever make use of it. However, it can assist in further improving performance for high-traffic, dynamic websites.

## Introduction

MySQLTuner is a useful tool for identifying potential performance bottlenecks in a MySQL server and providing recommendations for improving performance and security.

This article will help guide you through installing and using MySQLTuner on your GridPane servers, and the guidelines in this article are specific to WordPress.

### Table of Contents

 

## IMPORTANT: Before You Begin

MySQLTuner should only be used once your WordPress databases themselves are already optimized as much as possible. This includes:

Running MySQLTuner before optimizing your databases isn’t going to get you optimal results.

### Start Optimizing

If your databases haven’t yet been optimized, these articles may be helpful:

Be sure to backup your WordPress databases before performing any kind of optimization.

### Redis Object Caching

Redis object caching is included on all GridPane plans, even the free core plan. It will provide a massive performance boost for highly dynamic WordPress websites.

 

## What is MySQLTuner?

MySQLTuner is a popular open-source script that analyzes the configuration and performance of a MySQL database server. It provides recommendations for improving performance and security, based on the specific configuration of the MySQL server and the workload it is handling.

MySQLTuner works by analyzing various aspects of the MySQL server, such as the configuration variables, memory usage, query cache, and thread usage. It then provides a report with suggestions for optimizing the server’s performance.

Some of the specific areas that MySQLTuner analyzes include MySQL configuration variables, memory usage, query cache, and thread usage.

 

## Tuning MySQL Settings

Tuning MySQL configuration is an essential step in optimizing the performance of your MySQL database. MySQL has a variety of configuration variables that can be adjusted to suit the specific needs of your website or application.

Here are some of the most important variables to consider:

It’s important to note that changing MySQL configuration variables can have unintended consequences and should be done with care. It’s also important to monitor the performance of your MySQL database after making changes to ensure that they have the intended effect.

 

## Step 1. Connect to Your Server

To download and run MySQLTuner you will need to connect to your server via SSH as the root user. If this is your first time connecting to your server, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Download MySQLTuner

Download the MySQLTuner script with the following:

```
wget https://raw.githubusercontent.com/major/MySQLTuner-perl/master/mysqltuner.pl
```

### Make MySQLTuner executable

Change the permissions of the MySQLTuner script to make it executable. You can do this by running the following command:

```
chmod +x mysqltuner.pl
```

 

## Step 3. Run MySQLTuner

To run MySQLTuner you will need to MySQL administrator password.

### Copy the MySQL Password

You can view your password with the following GP-CLI command:

```
gp mysql get-pass root
```

### Run MySQLTuner

To run MySQLTuner, simply execute the MySQLTuner script with Perl:

```
perl mysqltuner.pl
```

### Enter MySQL Credentials

Enter your MySQL credentials – the administrative login is “root”.

```
Please enter your MySQL administrative login: root
Please enter your MySQL administrative password:
```

 

## Step 4. Review MySQLTuner Recommendations

MySQLTuner will generate a report with it’s recommendations for improving the performance  of your database/s. You’ll find the recommendations at the bottom of the output:

```
-------- Recommendations ---------------------------------------------------------------------------
General recommendations:
Check warning line(s) in /var/log/mysql/error.log file
Check error line(s) in /var/log/mysql/error.log file
Reduce your overall MySQL memory footprint for system stability
Dedicate this server to your database for highest performance.
Reduce or eliminate unclosed connections and network issues
Configure your accounts with ip or subnets only, then update your configuration with skip-name-resolve=1
Buffer Key MyISAM set to 0, no MyISAM table detected
Before changing innodb_log_file_size and/or innodb_log_files_in_group read this: https://bit.ly/2TcGgtU
Variables to adjust:
*** MySQL's maximum memory usage is dangerously high ***
*** Add RAM before increasing MySQL buffer variables ***
skip-name-resolve=1
key_buffer_size=0
innodb_log_file_size should be (=16M) if possible, so InnoDB total log file size equals 25% of buffer pool size.
```

The Variables to adjust in the above code block will typically always be shown. These can all be ignored (some context on each of these can be found below), and in Step 5, we’ll take a look at settings that may want to adjust should MySQLTuner recommend them.

### “Variables to Adjust” – What You Can Ignore

 

## Step 5. Adjusting MySQL Settings

The following are the variables that you’ll want to consider adjusting:

Before you make your changes, it’s advisable to make a copy of your mysql.cnf so you that you can return it to it’s default setting if ever needed:

```
cd /etc/mysql/mysql.conf.d/mysqld.cnf /etc/mysql/mysql.conf.d/mysqld.cnf_original
```

If making changes to the mysql.cnf directly, make one change at a time, and then run the following to stop and start MySQL:

```
gp mysql stop
```

```
gp mysql start
```

Below details how to make changes using GP-CLI. This will stop and start MySQL for you.

 

### innodb_buffer_pool_size

Ideally, the innodb_buffer_pool_size would be the same size as your collective WordPress databases. You change it with the following command:

```
gp stack mysql -innodb-buffer-pool-size {value}
```

Example:

```
gp stack mysql -innodb-buffer-pool-size 2048
```

 

### max_connections

You can change max_connections with the following:

```
gp stack mysql -max-connections {value}
```

Example:

```
gp stack mysql -max-connections 151
```

 

### GP-CLI for MySQL Configuration

Our available CLI for configuring your MySQL server (including more context on the above commands) can be found in this article:

Configure MySQL

 

## Step 6. Repeat Periodically

As you’re already taking the time to run MySQLTuner, it’s a good idea to run it periodically to ensure your MySQL server runs optimally. Once a week is often a good time frame.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

