# How to Reset WordPress User Roles with GP WP-CLI | GridPane

# How to Reset WordPress User Roles with GP WP-CLI

 

2 min read 

## Introduction

In rare circumstances, a plugin or a migration gone wrong could corrupt WordPress user data in your website’s database.

This can result in odd behavior such as redirecting you back to the homepage, or the “Sorry, you are not allowed to access this page” error.

In this article we’ll take a look at how you can confirm and fix this issue using GP WP-CLI, which you can learn more about here.

 

## Step 1. Connect to Your Server

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Check User Permissions

First, we need to check the website’s user permissions with the following GP WP-CLI command (replacing “site.url” with your domain name):

```
gp wp site.url user list
```

You will see an output similar to below. On lines 14 and 15 you can see my websites user, including the ID:

 

```
root@aws-nginx-mariadb:~# gp wp examplewebsite.com user list
#####################################################################################################
The following command was run at Wed Apr 14 18:54:29 UTC 2021 with PID: 10765... /usr/local/bin/gp wp examplewebsite.com user list
#####################################################################################################
GridPane Developer
Validated... running /usr/local/bin/gp script...
Processing GridPane WP-CLI command to examplewebsite.com...

**********************************************************************************************
gp-wpcli Log Begin - examplewebsite.com
**********************************************************************************************
Wed Apr 14 18:54:29 UTC 2021

ID      user_login      display_name    user_email      user_registered          roles
1       ste-bell        ste-bell        ste@bell.com    2021-04-14 18:53:33     

**********************************************************************************************
gp-wpcli Log Begin - examplewebsite.com
**********************************************************************************************
```

You can see that there isn’t a user role at the end of the line. If it was correct, it would look as follows:

 

```
ID      user_login      display_name    user_email      user_registered          roles
1       ste-bell        ste-bell        ste@bell.com    2021-04-14 18:53:33      administrator
```

## Step 3. Reset the User Role

Next, we need to reset the user role. You can do this with the following command (again switching out “site.url” for your domain name). After “set-role” the number 1 refers to the user ID. Your user may have a different ID number so be sure to use the correct one.

```
gp wp site.url user set-role 1 administrator
```

 

```
root@aws-nginx-mariadb:~# gp wp examplewebsite.com user set-role 1 administrator
#####################################################################################################
The following command was run at Wed Apr 14 19:09:38 UTC 2021 with PID: 13043... /usr/local/bin/gp wp examplewebsite.com user set-role 1 administrator
#####################################################################################################
GridPane Developer
Validated... running /usr/local/bin/gp script...
Processing GridPane WP-CLI command to examplewebsite.com...

**********************************************************************************************
gp-wpcli Log Begin - examplewebsite.com
**********************************************************************************************
Wed Apr 14 19:09:38 UTC 2021

Success: Added ste-bell (1) to http://examplewebsite.com as administrator.

**********************************************************************************************
gp-wpcli Log Begin - examplewebsite.com
**********************************************************************************************
```

### Role Doesn’t Exist Error

If you encounter the following error:

```
Error: Role doesn't exist: administrator
```

To fix this, run the following command to reset the role:

```
gp wp site.url role reset administrator
```

You will now be able to run the reset command again:

```
gp wp site.url user set-role 1 administrator
```

And you’re now all set!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

