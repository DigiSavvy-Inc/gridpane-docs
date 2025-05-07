# Connect to a WordPress Database Remotely With a Desktop MySQL Client | GridPane

# Connect to a WordPress Database Remotely With a Desktop MySQL Client

 

5 min read 

## Introduction

This tutorial provides a step-by-step guide to connecting the tool of your choice with your GridPane WordPress site databases. To complete this tutorial, you will need to have downloaded and installed one of the free tools listed below and have a GridPane server provisioned with a site installed.

### Table of Contents

 

## Tools for the Job

With GridPane you can choose to use the MySQL Database management tool of your choice to work with your GridPane-managed WordPress site databases, we provide a PHPMyAdmin integration that allows you to connect to your Database from within your browser, or alternatively, you may use one of the many available desktop MySQL management solutions.

If you would like to use GridPane’s PHPMyAdmin integration, then we have an easy-to-follow guide here, if you would prefer to use a desktop client, then read on.

### Database Management Tools

There are several high-quality free desktop DB management tools available no matter which platform you are using, including:

In this documentation, we are learning how to connect to our remote database with a client via SSH on Port 22. This is our recommended way to connect from an external client due to the higher security offered by SSH.

 

## Percona vs MariaDB

While Percona is still using root password access, MariaDB moved to do away with using Root Password Access locally, and they are now using the Unix Socket.

This was introduced in 10.4:

The credentials you use to connect to each type of database are different.

 

 

### Information

If you're not sure whether you're server is using Percona or MariaDB, you can quickly check by navigating to the Servers page inside your GridPane account and clicking on the name of your server. This will open up the server customizer which will display your server's stack like so:

## Step 0. Add Your SSH Key to GridPane

To follow along with this article, you’ll need to have added your SSH Key to the server that is hosting the database that you wish to manage. If this is your first working with SSH, these articles will help you get set up:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Add/Remove an SSH Key to/from an Active GridPane Server

 

## Step 1. Open Your Database Management Client

In this tutorial we will be using Sequel Pro to connect to our database, however, most of the available tools are very similar and have directly analogous configurations.

Open your Database management client and navigate to the connection configurations for SSH connections to a remote database. In Sequel Pro, that looks like this:

To connect to our database, we will need to provide the following configuration details.

For Percona:

Port Number is optional and defaults to Port 3306. As we will be connecting by SSH Port 22, we do not need to specify the port number nor open Port 3306 in the GridPane Site Customizations Panel.

 

## Step 2. Get Database Configuration Details

First, head over to the Sites page inside your GridPane account:

### Open the WebSite Customizer

In the Active Sites panel, click on the domain in the URL column to open the Site Customization pop-up box for the site for which you wish to manage the database.

Return to GridPane and the website customizer from Step 3. above. This time, locate the Display wp-config button and click it:

GridPane will retrieve your wp-config file and display its contents in a popup modal window. You will need to make note of your WordPress site MySQL database settings:

Take note of the following connection configuration details that the desktop MySQL client requires:

 

 

### Information

Your DB_HOST will be set to localhost. Some DB clients require you to replace localhost with the IP 127.0.0.1.

## Step 3. Configure Your Desktop Client and Connect

The desktop MySQL management client requires an SSH host to make the SSH connection, this is the IP address of the server hosting the database. The images below are for Sequel Pro, but all these tools are similar.

### 3.1 Copy Your IP Address

You can get the IP address by copying it from the IP column of your site in the active site’s panel:

Alternatively, if you click on the copy button beside the IP address, it will be automatically copied to your computer’s clipboard.

### 3.2 Configure Your Database Client

Configure your client using the details you have taken note of in Step 5. and Step 6. above. For SSH User on Percona, enter root.

For MariaDB, you will need to choose “Socket” and then enter the socket path:

```
/run/mysqld/mysqld.sock.
```

Most Clients will allow you to connect by SSH using either a key pair or password. GridPane will only allow SSH root connections with the more secure key pair method.

Depending on your client there will be an option to browse to locate your machine’s private SSH key. In Sequel pro, it means clicking on the little key icon next to the SSH Password box.

A pop-up window will appear and allow you to browse your system to the directory containing your SSH Key pair.

Remember, your server has the public id_rsa.pub key, so you need to select your private id_rsa key from your SSH Key Pair.

Your key location should appear in your client’s SSH Key input field. In Sequel Pro the SSH Password field has been replaced with a completed input field showing the location of my private key.

With the connection configurations completed, you can now click connect.

### 3.3 Manage Your Database

Your MySQL client will connect to your database, and you can manage your WordPress database securely, and with ease, using the tools and features provided.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

