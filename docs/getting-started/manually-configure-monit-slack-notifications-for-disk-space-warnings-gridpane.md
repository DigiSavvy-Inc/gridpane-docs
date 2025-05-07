# Manually Configure Monit/Slack Notifications for Disk Space Warnings | GridPane

# Manually Configure Monit/Slack Notifications for Disk Space Warnings

 

4 min read 

## Introduction

Ensuring that you have enough free disk space is extremely important for your servers health. Reaching maximum capacity can have catastrophic consequences, including the corruption of MySQL, so it’s important only to adjust these notifications on servers that have A LOT of disk space.

For servers where it does make sense to adjust these notifications (for example you have a TB of disk space but you’re receiving 80% disk space warnings), this article will show you how you can adjust them.

### Table of Contents

 

## About Disk Space Warnings

GridPane will automatically notify you once your server disk space exceeds 80% capacity. This first notification happens one time, and then another will happen if your disk spaces exceed 85% capacity. This is a good time to start looking at freeing up some space on your server.

After 90%, notifications will start happening with increased frequency until the issue is resolved. This is where issues can start to happen as your system needs some free disk space to operate efficiently.

If you exceed 90% then it’s really time to look at either freeing up some space, or increase the size of your server.

By the time you get above 95% you may begin experiencing major issues to the point where your server simply can’t function properly anymore.

These settings are pretty ideal as they are, and it’s not at all necessary to change them. However, we have received a couple of requests on how to go about setting up your own disk space warnings, and this article was created.

 

## Step 1. SSH Into Your Server

To get started, please see the following articles:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Step 2. Set Your Notifications

The disk space notifications are handled in /etc/monit/conf.d/filesystem. To view them, run the following command:

```
cat /etc/monit/conf.d/filesystem
```

The notification settings look as follows:

```
CHECK FILESYSTEM system PATH /  if space usage > 80%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 80 warning"  if space usage > 85%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 85 warning"  if space usage > 90%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 90 warning"    AND repeat every 60 cycles  if space usage > 95%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 95 warning"    AND repeat every 30 cycles  if space usage > 98%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 98 error"    AND repeat every 5 cycles  if space usage > 99%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 99 error"    AND repeat every 1 cycles
```

As you can see above, the 90% and above warnings each contain an instruction to repeat every X cycles. To translate that, this line is telling Monit/Slack to send a notification every X minutes, with 1 cycle equaling 1 minute.

You can use the syntax above to craft your own notifications. For example, to set a notification for when a server goes over 70%, you could add the following two lines:

```
if space usage > 70%then exec "/usr/local/bin/gpmonitor FILESYSTEM 70 warning"
```

If you wanted to setup a notification for once per day at 75% you could add:

```
if space usage > 75%then exec "/usr/local/bin/gpmonitor FILESYSTEM 75 warning"AND repeat every 1440 cycles
```

1440 being equal to the minutes in one day.

### Adding our new notifications

Now that you’ve decided what notifications you’d like to set up, we need to edit the file with the following command:

```
nano /etc/monit/conf.d/filesystem
```

Here’s how mine looks with our 2 rules for 70% and 75% added (leaving the rest as they are by default):

```
CHECK FILESYSTEM system PATH /  if space usage > 70%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 70 warning"  if space usage > 75%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 75 warning"    AND repeat every 1440 cycles  if space usage > 80%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 80 warning"  if space usage > 85%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 85 warning"  if space usage > 90%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 90 warning"    AND repeat every 60 cycles  if space usage > 95%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 95 warning"    AND repeat every 30 cycles  if space usage > 98%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 98 error"    AND repeat every 5 cycles  if space usage > 99%    then exec "/usr/local/bin/gpmonitor FILESYSTEM 99 error"    AND repeat every 1 cycles
```

Make sure your syntax is correct:

We now need to save the file with CTRL+O followed by Enter, and then exit nano with CTRL+X.

 

## Step 3. Reload Monit

To make your changes take effect, you need to reload Monit with the following command:

```
monit reload
```

Nice work! You’re all set.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

