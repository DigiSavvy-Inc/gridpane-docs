# How to change a System User Password | GridPane

# How to change a System User Password

 

1 min read 

From time to time you may need to update the password for your system users. To get started, login to your account and click through to your system users page:

Next, scroll down to the bottom and find the user that you wish to edit. If you have many system users, you can use the search bar to search to narrow down the results.

Then click on the padlock button to open up the password change modal.

Here you can enter your new password. Hit the Change Password button to complete the process and you’re all set!

 

## Change a System User Password via the Command Line

If you’d prefer to change the password on the command line, SSH into your server and then run the following command (switching out “username” for your System User):

```
passwd username
```

For example:

```
passwd mysystemusername
```

 

## Change the default “gridpane” System User Password

If you need to change the password for the default gridpane user, you can do so with the command below.

Please note that this is now legacy and we strongly recommend that you keep your websites on their own unique system users that are NOT the “gridpane” user.

However, we are still asked how to change the password for this user from time to time and this the command you can use to do so:

```
passwd gridpane
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

