# How to Upgrade Monit from Version 5.25 to 5.26 (if 5.26 Failed to Install) | GridPane

# How to Upgrade Monit from Version 5.25 to 5.26 (if 5.26 Failed to Install)

 

3 min read 

 

### Information

If you've created a new server and Monit is giving a 502 error due to the version being 5.25, this is something that our support team will fix for you if you create a support ticket/community forum post. However, for those of you who would prefer to simply fix the issue yourself, this article details the procedure.

## Introduction

If Monit isn’t working on your newly created server and you’re seeing a 502 error when trying to access it, this likely means that Monit 5.26 failed to install. This can happen during the server build if for some reason it fails to download Monit directly from the Monit Git, and your server is left with Monit installed from the Ubuntu repo, which is out of date.

This needs to be corrected, and this guide will walk you through how to install and configure the version 5.26.

To follow the steps below you’ll need to SSH into your server. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Checking Monit

Check Monit’s status with:

```
service monit status
```

If it’s down for any reason, this may be the source of the issue you’re experiencing and not.

### Check Monit’s version

Check which version of Monit is installed with:

```
monit --version
```

Here’s the output you may see:

```
root@vultr-server:~# monit --versionThis is Monit version 5.25.1Built with ssl, with ipv6, with compression, with pam and with large filesCopyright (C) 2001-2017 Tildeslash Ltd. All Rights Reserved.
```

5.25 is the fallback version. GridPane uses Monit 5.26, so if the correct version is installed the output will be this instead:

```
root@gpserver:~# monit --versionThis is Monit version 5.26.0Built with ssl, with ipv6, with compression, with pam and with large filesCopyright (C) 2001-2019 Tildeslash Ltd. All Rights Reserved.
```

If your server has Monit 5.25 installed, below is how to correct this.

 

## Step 1. Download and Install Monit 5.26

First, navigate to the /opt/gridpane directory:```
cd /opt/gridpane/
```

### Download and Install

Next, run the following 5 commands to download and install Monit 5.26:

```
wget https://mmonit.com/monit//dist/binary/5.26.0/monit-5.26.0-linux-x64.tar.gz
```

```
tar zxvf /opt/gridpane/monit-5.26.0-linux-x64.tar.gz
```

```
rm /opt/gridpane/monit-5.26.0-linux-x64.tar.gz
```

```
cp /opt/gridpane/monit-5.26.0/bin/monit /usr/local/bin/
```

```
cp /etc/monit/monitrc /etc/
```

Monit is now installed.

### Set Permissions

Next, set the correct permissions for the above file:

```
sudo chmod 0700 /etc/monitrc
```

### Copy to: /usr/local/bin

The next thing is to make sure that all files are in the correct place. Run the following:

```
cp /etc/monit/monitrc /usr/local/bin
```

 

## Step 2. Configure Monit to Read the Correct Script

Now that Monit 5.26 is installed, we now need make sure Monit reads the script in /usr/local/bin/monit instead of /usr/bin/monit to avoid an error like this:

monit.service: Failed at step EXEC spawning /usr/bin/monit: No such file or directory

Run the following

```
nano /lib/systemd/system/monit.service
```

Replace /usr/bin/monit with /usr/local/bin/monit so the file contents is as follows:

 

```
[Unit]
Description=Pro-active monitoring utility for unix systems
After=network-online.target
Documentation=man:monit(1) https://mmonit.com/wiki/Monit/HowTo

[Service]
Type=simple
KillMode=process
ExecStart=/usr/bin/monit -I
ExecStop=/usr/bin/monit quit
ExecReload=/usr/bin/monit reload
Restart = on-abnormal
StandardOutput=null

[Install]
WantedBy=multi-user.target
```

### Complete Installation

Run the following four commands to complete the installation:

```
systemctl daemon-reload
```

```
systemctl restart monit
```

```
monit reload
```

If you experience an error, see the section below. If no error, reload Nginx:

```
gp ngx reload
```

 

## Error when reloading Monit?

You may encounter this error when running monit reload:

```
root@server:~# monit reload/etc/monit/conf.d/system:3: syntax error 'core'
```

If this is the case, you would need to remove the monit in /usr/bin and then symlink the one in /usr/local/bin to /usr/bin. Run the following two commands:

```
rm /usr/bin/monit
```

```
ln -s /usr/local/bin/monit /usr/bin/monit
```

### Now reload Monit and Nginx:

```
monit reload
```

```
gp ngx reload
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

