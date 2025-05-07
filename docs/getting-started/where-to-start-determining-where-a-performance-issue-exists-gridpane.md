# Where to Start Determining Where a Performance Issue Exists? | GridPane

# Where to Start Determining Where a Performance Issue Exists?

 

3 min read 

## Introduction

GridPane offers numerous tools for debugging performance-related issues, as well as many detailed guides here in our knowledge base.

In this short article, we’ll cover the first steps you should take and link to further resources.

### Quick Tools Overview

At GridPane you have easy access to:

With full root access to your server you can also use the top and htop utilities installed on your server.

 

## Check “top” and “htop”

If your site/server feels sluggish, the first thing to do is login as root via SSH (you will need an SSH key). Then run the “top” command or the “htop” command. If this is your first time connecting to your server, please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### top

First, run the top command (copy and paste, hit enter):

```
top
```

Your load should be less than 1.00 X the number of CPU cores of your server. For example, if you have a two CPU core server, your load should generally be below 2.00.

Additionally, if top shows 50% or more in id (idle) resources, then your server is healthy, and you should be looking within the site for errors and code bottlenecks.

All of the metrics you’ll see in top are in the form of percentages. 100% equals 1 CPU core of the server. For example, if you see MySQL taking up 200% and you have a 2 CPU core server, SQL would be taking up all of your CPU resources.

##### CPU Steal

On the right of the highlighted section in the screenshot above, you can see a metric marked “st“. This stands for “steal”, and if your seeing a high percentage of steal, you should contact your server provider as it means that someone else’s VPS is infringing on your resources.

##### PHP Processes

You may see many PHP processes overwhelming your server. If you do, it may mean that a site needs to have its number of PHP workers lowered to maintain server stability, or it may mean a plugin is misbehaving and looping.

You can exit top with Q or CTRL+C.

Here’s a more detailed guide on the top command: How to use the top command to monitor system processes and resource usage

### htop

top and htop cover a lot of the same information, but htop can make it easier to assess CPU usage and the active processes on your server.

You can usehtop with:

```
htop
```

You can exit htop with Q or CTRL+C.

Learn more about htop in this article: How to use the htop command to monitor system processes and resource usage

 

## Next Steps

Our guide on troubleshooting 504  issues and performance issues is a detailed guide that applies to essentially every “website/server is slow” type of problem. Learning the contents of this article will dramatically improve your skills and confidence as a self-managed host:

Diagnosing 504 Timeouts and Performance Issues

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

