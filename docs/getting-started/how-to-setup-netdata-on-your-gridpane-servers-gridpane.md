# How to setup Netdata on your GridPane Servers | GridPane

# How to setup Netdata on your GridPane Servers

 

4 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

### Table of Contents

 

## Introduction

Netdata is a very cool (and totally FREE!) server monitoring tool and alert system. We’ve recently been asked about it, and while we can’t provide support for it, for those of you who are interested in checking it out, this guide is for you.

Also, big thanks to “WordPresseh” for contributing the original knowledge base article to the GridPane community. That was awesome, thank you.

 

 

### IMPORTANT

Before we begin, we need to reiterate that this is a third party app and is NOT supported by GridPane. Please review the following guide to understand how it could potentially impact our ability to provide support for any servers you install it on:

Can I install other Applications on a GridPane managed server?

## Part 1. Install Netdata on your server

Installing Netdata is a simple process that only takes a few minutes. Below are the steps to install it on your server/s.

### Step 1. SSH into your server:

Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Create a new user

For simplicity, I’m going to create a user called “netdata” and install Netdata via this user. You can switch out “netdata” in the commands below for any username you prefer.

To start run:

```
adduser netdata
```

You’ll then be prompted to enter a new password and then confirm the password you just entered.

Next, you can simply hit enter for the next few questions.

Finally, you’ll be asked to confirm the details you’ve just entered. Type y and Enter.

Your new user has now been created.

Next, run the following command to add the new user to the sudo group:

```
usermod -aG sudo netdata
```

Finally, switch to your new user with:

```
su - netdata
```

### Step 3. Install Netdata on your server

To install, run the following command:

```
bash <(curl -L -Ss https://my-netdata.io/kickstart.sh)
```

The above will install Netdata.

If you have any issues with the above command, this is an alternative:

```
wget -O /tmp/netdata-kickstart.sh https://get.netdata.cloud/kickstart.sh && sh /tmp/netdata-kickstart.sh
```

Follow the prompts during the setup process, and once installation is complete you’ll see the following:

### Step 4. Opt out of anonymous statistics

According to their documentation, running the above installation script with --disable-telemetry is supposed to opt you out of their data tracking automatically. In my testing, however, this didn’t work, so we’ll do this the long-winded way.

To opt out of anonymous statistics, navigate to the Netdata directory with:

```
cd /etc/netdata
```

Switch back to root user with:

```
sudo -s
```

And run the following command to opt out:

```
touch .opt-out-from-anonymous-statistics
```

For more information check out their article on anonymous statistics here:

https://learn.netdata.cloud/docs/agent/anonymous-statistics

 

## Part 2. Connect your server to Netdata Cloud

Now we just need to connect your server to Netdata Cloud and you’re all set!

### Step 1. Create a Netdata Cloud account

Head to https://app.netdata.cloud/sign-in

Enter your email, confirm your email, then head back and sign into netdata.cloud.

### Step 2. Sign into Netdata Cloud and copy your claim script

On signing in, you’ll be presented with a page that looks like the following:

Choose the “War Room” you wish to add your server to from the dropdown and copy your claim script.

### Step 3. Claim your server

Back in your server, paste in your key, and hit enter.

You’ll see a message like this in the image below:

Nice job! You’ve successfully set up Netdata on your server. Back in netdata.cloud, you’ll be able to see your server stats via their very cool dashboard:

 

## Part 3. Netdata Resources

For Netdata’s step-by-step user guide, check out:

https://learn.netdata.cloud/guides/step-by-step/step-00

If at any point in the future, you would like to uninstall Netdata, check out their guide here:

https://learn.netdata.cloud/docs/agent/packaging/installer/uninstall

There’s tons of documentation on their site. Go crazy.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

