# How to Use the htop Command to Monitor System Processes and Resource Usage | GridPane

# How to Use the htop Command to Monitor System Processes and Resource Usage

 

8 min read 

### Table of Contents

 

## Introduction

htop is the prettier, more colorful, and slightly more up-to-date version of top. A few metrics such as steal and iowait are easier to see in top, but for most other purposes, htop may be the better tool for troubleshooting server performance issues.

Here is our article on top, we’d recommend you start there and then come back to htop if you haven’t already read this:

How to use the top command to monitor system processes and resource usage

Just like top, this is an excellent skill to develop and will help assist you in diagnosing any performance issues on your websites and server. It’s easy to use once you know the basics.

The goal of this article is to get you to a place where you can run the htop command on your server and understand the information that it’s displaying. Armed with this information, you’ll be able to troubleshoot any performance issues you discover.

 

## What Can “htop” Show You?

htop will display a real-time overview of what’s happening on your server. In a nutshell, you’ll be able to see the following at a glance: –

 

## Getting Started

A note on system users – we highly recommend putting each of your websites on their own system user. Not only is important to keep your websites isolated from each other (a hacked/malware-infected website can’t affect sites on a different system user), it will also show in the USER column, so you can easily identify any site with high resource usage using either top or htop.

For example, if my website was assigned to a system user called “steve-com”, in the USER column, you’ll see the user “steve-com” and know exactly which site you need to look into. If they were all on the same system user, you won’t be able to tell what’s going on.

To run the top command you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Once inside your server, run:

```
htop
```

To exit htop use Q or CTRL+C.

 

## Part 1. The “htop” Summary Area: What it All Means

The summary area at the beginning is the system overview. Below we’ll cover what each part means, section by section.

### CPU Breakdown

Here, with the numbers 1 and 2, we can see this is a 2-core VPS. A 4 core will have 4 bars, 8 core = 8 bars, and so on. Each number/bar represents one CPU. Each bar has a % on the right-hand side indicating how much CPU is in use.

Specific CPU usage is then broken down by processes via the following color code:

Bonus points: –

top maybe easier to understand in terms of what exactly is consuming CPU, but what we’re looking to see is just how busy are the CPU/s. In this article, the bars are mostly empty, which means the CPU is mostly idle.

The higher your CPU usage (full bars, higher percentage), the busier your system is, and this will affect the performance of your websites.

Bursts of high usage are normal and nothing to be concerned about. Sustained high CPU usage is something that requires further attention.

### RAM and Swap Usage

This section shows information regarding the memory usage of the system. We have RAM and Swap – Swap is part of your hard disk that’s used by your server like it uses RAM. This is why having spare disk space is important for your system and why performance issues can arise when your disk space usage gets past 90%. If you use software such as Photoshop, Illustrator, or other heavy Adobe Creative Cloud apps, you’ll likely have experienced the same thing on your computer.

RAM usage is broken down by colors.

Swap space is your safety net if you run out of RAM. High swap and RAM usage will affect your system’s ability to process tasks efficiently, potentially resulting in 504 time-out errors. Processes will get slower and backed up while they wait for memory to become available.

### Tasks

For clarity, Tasks and Processes for our purposes are the same things. Here we have 44 total processes, with 1 currently running. 100 “thr” means “threads”. So here we have 44 tasks that are broken up into 100 threads.

### Load Average

This is the exact same breakdown that the top command gives. If you haven’t already read that article, please check it out (link at the top and bottom of this article). In a nutshell, here we can see the average “load” over one, five, and fifteen minutes.

Load is measured per CPU, so if you have more than one core, you will need to divide what you see by the number of cores your server is running. Sustained, high load times mean your server is consistently busy. This could be due to a number of reasons, such as high website traffic or a brute force attack. The rest of the data provided by htop should help fill in the gaps.

### System Uptime and Current System Time

Here you can see how long the server has been online and the current system time. For our purposes, this isn’t particularly important.

 

## Part 2. Active Processes

So you now have an overview of what’s happening on your server at a glance. If you’re seeing high resource usage, we now need to look at the processes themselves to see what’s responsible.

The active process list is the lower part of the overview. This is highlighted below:

Below is a quick breakdown of what each column displays: –

Below these in the footer are htop‘s menu items. More on these below.

 

## Part 3. “htop” Commands

Before anything else, you can scroll the process list with the arrow keys – vertically and horizontally. This will come in handy as you get to know the basics.

### The bottom menu

You can exit any of the following commands by hitting Esc.

### Awesome Shortcuts

You can use any of the following shortcuts simply by pressing them on your keyboard. There are more available (press F1 for more details while inside htop), but for troubleshooting purposes, these are the main ones you’ll want to learn.

 

## Part 4. Using the Data Inside “htop” to Troubleshoot Performance Issues

The commands in part 4 can yield a lot of information to help you pinpoint performance issues. You’ll likely find that you’ll use F3, F4, F9, u, p, m, and t when you’re inside htop.

What we’re looking for here is what tasks in the COMMAND column are using the most CPU% and MEM%. Once we know this, we can begin further diagnosis.

For example, if you’re seeing high PHP usage, it’s possible your server is experiencing a brute-force attack. Using the above commands, you should be able to narrow down a specific website and take action accordingly.

High MySQL may indicate database table locking or lack of proper caching.

 

## Further Reading

If you haven’t already read the top article, we highly recommend you do so. Learn more about htop and further troubleshooting in the following guides:

You may also want to check out the Security and Performance sections of our knowledgebase here:

You can also learn more about top directly on your server with:

```
man htop
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

