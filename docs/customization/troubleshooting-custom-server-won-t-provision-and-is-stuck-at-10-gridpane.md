# Troubleshooting: Custom Server Won’t Provision and is Stuck at 10% | GridPane

# Troubleshooting: Custom Server Won’t Provision and is Stuck at 10%

 

3 min read 

### Table of Contents

 

## Introduction

Having a server fail to provision can be frustrating, but hopefully the tips in this article will help you get yours up and running.

Before anything else, these are generally when we see servers fail on the rare occasions that they do:

You can learn more about this here: Why do some servers fail to provision correctly?

If your server didn’t fail at 10%, then it’s likely that everything you set up was correct. You may need to simply repeat the process as it was likely a minor repo outage.

If it did fail at 10%, continue below.

 

## Troubleshooting Tips

The following 3 tips are the most common issues that we see with servers that are failing to get past the 10% mark.

 

### 1. Check your Ports

First, check ports 22, 80, and 443 are definitely open – they aren’t always open by default on some providers, and some require these to set manually via ingress rules (Oracle and IBM for example).

If you’re unsure, search for your host and “ingress rules” in Google to check for their documentation.

You can check your ports with the following command:

```
nc -zv <IP> <PORT>
```

For example:

```
nc -zv 199.199.199.99 22
```

Simply repeat for each port. This can be run from any server.

 

### 2. Did you use the correct Ubuntu Version?

GridPane requires Ubuntu 20.04 LTS or 22.04 LTS. Our stack won’t work with a minimal version or any other Ubuntu version (we get asked this one a lot).

If the provider you’re using only offers minimal images and not full Ubuntu 20.04 LTS, you can install the minimal version, and then on the server run the following command before our provisioning code:

```
sudo apt install ubuntu-server
```

After this, proceed as normal.

 

### 3. Provisioning code ran as the root user?

Did you definitely run our provisioning code as the root user? Depending on the provider, they may log you in as a system user that they themselves have created.

Before pasting our provisioning code, first run:

```
sudo -s
```

OR

```
sudo sh
```

 

### 4. Arm64-architecture is Not Supported

ARM servers are not supported by GridPane, and these typically require application versions to be compiled for it in most cases. Most providers don’t offer this as an option.

 

## The Provisioning Code Results in an Error

If you’re seeing an error after entering our provisioning code, the provider’s console is likely making a mess of the formatting.

We see this with Hetzner from time to time, changing “https://” to “https;//” for example, or appending http:// before https:// like this:

```
http://https://provisioningcode…..
```

Hit the up key to check the code, and correct the mistakes. Hit Enter to run the code again when you’re ready.

 

## Your Servers IP Address Has Been Banned by Google Cloud

This is another issue we’ve seen with Hetzner in the past, but it’s certainly possible that other providers could experience this too – especially if their pricing is considerably lower than most competitor offerings. To check that your server can connect to our platform, run the following:

```
curl my.gridpane.com
```

Contact your server provider to report the issue if this doesn’t return some basic HTML. Unfortunately, there’s nothing that we can do to help fix this issue.

 

## Starting Over

It’s better to start with a fresh server, however, you can try the following steps on the failed server if you’d like to first retry:

### Step 1

First, delete the server out of the GridPane UI.

### Step 2

On the server, run the following command:

```
rm -r /opt/gridpane
```

### Step 3

Add the server back to the UI.

### Step 4

Run the new provisioning command.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

