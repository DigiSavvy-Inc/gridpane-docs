# Change password of a database user | GridPane

# Change password of a database user

 

2 min read 

### Table of Contents

 

## Introduction

In the highly unlikely event that you need to change the password of a website’s database, this article will walk you through how to do so. It’s a simple copy and paste exercise.

For this, you’ll need to connect to your server – if this is your first time, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 1. Login to MySQL

The following command will directly log you into MySQL. Simply copy and paste it and hit enter:

```
gp mysql login root
```

 

## Step 2. Update Your Site’s MySQL User Password

Copy and paste the following, and edit the highlighted parts in red to match your website’s database user name and the new password you want to set (you can view this inside your wp-config.php file inside your websites customizer):

```
ALTER USER 'website-db-user-here'@'localhost' IDENTIFIED BY 'new-password-here';
```

Exit MySQL with:

```
exit
```

 

## Step 3. Change the Database Password on the Website

The following command will change your website’s database password inside of your wp-config.php and site.env files.

Modify the following command to replace “new-password-here” with your new password, and “site.url” with your website URL:

```
gp conf write db-pass new-password-here -site.env site.url
```

Here’s an example of how this looks:

```
gp conf write db-pass Z&wp?iwfoM;sW3RYA@E]O -site.env mywebsite.com
```

When ready to go, paste the command line and hit Enter.

 

## Step 4. Reset PHPMyAdmin Credentials

To finish up, you’ll now need to run the following command to update PHPMyAdmin (again, replace site.url with your actual site URL):

```
gp site site.url -dbcreds
```

And that’s it! You’re all set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

