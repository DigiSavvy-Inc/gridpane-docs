# How to Use the top Command to Monitor System Processes and Resource Usage | GridPane

# How to Use the top Command to Monitor System Processes and Resource Usage

 

10 min read 

### Table of Contents

 

## Introduction

One of the many great things about Linux is that it comes with system monitoring tools like top and htop built right in. In this article, we’ll dive into the top command and how you can use it to monitor your systems processes and resource usage. htop can actually be a better tool for pinpointing some performance issues, but both are necessary tools for your toolbox.

Learning this will help you in diagnosing any performance issues on your websites and server. As it’s a command line application, it’s not the most intuitive monitoring tool at first glance, but it is easy to use once you know the basics.

The goal of this article is to get you to a place where you can run the top command on your server and understand the information that it displays. Armed with this information, you’ll be able to see if anything requires your attention and then take action accordingly. For example, if you’re seeing a high steal rate, it’s likely that you have a noisy neighbor.

 

## What Can “top” Show You?

top will display a real-time overview of what’s happening on your server. In a nutshell, you’ll be able to see the following at a glance: –

 

## Getting Started

A note on system users – we highly recommend putting each of your websites on their own system. Not only is important to keep your websites isolated from each other (a hacked website can’t affect sites on another system user), but it will also show in the USER column, so you can easily identify any site with high resource usage using either top or htop.

For example, if my website was assigned to a system user called “steve-com,” in the USER column, you’ll see the user “steve-com” and know exactly which site you need to look into. If they were all on the same system user, all you’ll know is that one of your sites is spiking.

### Opening top

To run the top command you will need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

Once inside your server, run the following command to open top:

```
top
```

To exit top use Q or CTRL+C.

 

## Part 1. The “top” Summary Area: What it All Means

The summary area at the beginning is the system overview. Below we’ll cover what each part means, section by section.

### System time, server up-time, and user sessions

Here you can see the current system time, how long the server has been online, and the number of active user sessions. For our purposes, this isn’t particularly important.

 

### Load average

Here we can see the average “load” over one, five, and fifteen minutes.

Load is measured per CPU, so if you have more than one core, you will need to divide what you see by the number of cores your server is running.

For example, a load average of 0.5 on a single-core VPS means that the server is running at 50% capacity – 50% of the CPU is free, and the other is running tasks. A value of 2.5 would mean the server is overloaded with 150% more work than it can process.

On a two-core VPS, 0.5 would mean 50% of one core, which means the server is at 25% capacity and able to take on 75% more work. An average of 2 would mean 200% – 100% of each of its cores – so that VPS would be at 100% capacity.

Sustained, high load times mean your server is consistently busy. This could be due to a number of reasons, such as high website traffic or a brute force attack. The rest of the data provided by top should help fill in the gaps.

 

### System tasks breakdown

For clarity, Tasks and Processes for our purposes are the same things. Here we have 153 total processes.

If you check top regularly, tasks can be a good indicator of how busy your system is.

 

### Real-time CPU usage is broken down into categories

CPU usage is the primary metric we’re interested in.

The higher your %Cpu, the busier your system is, and this will affect the performance of your websites.

Bursts of high usage are normal and nothing to be concerned about. Sustained high CPU usage is something that requires further attention.

The following is a quick explanation of what each of these values means.

User (us)This is the CPU time used by userspace processes. These are your application-level processes, such as MySQL. This is going to be the biggest user of CPU.

System (sy)This shows the amount of CPU time used by the kernel. The kernel is responsible for low-level tasks that take care of your general day-to-day server processes, e.g. operating system processes.

This can spike when data is being read or written to disk. Sustained high usage may indicate a device driver issue.

Nice (ni) This is a subset of the “user” state and shows the CPU time used by processes that have a positive niceness (those with a lower priority than other tasks).

The default value is 0, and it ranges from 19 down to -20. 19 is the lowest priority. -20 is the highest priority.

Idle (id)Time spent in idle operations.

I/O Wait (wa)Time spent on waiting on IO peripherals, usually disk.

Hardware interrupt (hi)Time spent servicing hardware interrupt routines. These require immediate CPU attention.

Software interrupt (si)Time spent servicing software interrupt routines.

Steal (st)Steal only applies to virtual machines, not dedicated servers. Sustained steal can be a serious problem as it means that other instances on the shared server are stealing away from your allocation, which may cause performance issues.

 

### Real-time memory usage

This section shows information regarding the memory usage of the system. We have RAM and Swap – Swap is part of your hard disk that’s used by your server like it uses RAM. This is why having spare disk space is important for your system and why performance issues can arise when your disk space usage gets past 90%. If you use software such as Photoshop, Illustrator, or other heavy Adobe Creative Cloud apps, you’ll likely have experienced the same thing on your computer.

total, free, and used values are pretty much self-explanatory.

“buff/cache” are two different things lumped into one. Buff is data that’s in the process of being written, and this cannot be reallocated. Cache is data that’s been read and can be reallocated if needed.

“avail mem” is the amount of available memory that can be used without causing more swapping.

Swap space is your safety net if you run out of RAM. High swap and RAM usage will affect your system’s ability to process tasks efficiently, potentially resulting in 504 time-out errors. Processes will get slower and backed up while they wait for memory to become available.

 

## Part 2. Active Processes

So you now have an overview of what’s happening on your server at a glance. If you’re seeing high resource usage on your server, we now need to look at the processes themselves to see what’s responsible.

The active process list is the lower part of the overview and is sorted by CPU usage by default – the highest running processes at the top. This is highlighted below:

Below is a quick breakdown of what each column displays: –

 

## Part 3. Using the Data Inside “top” to Troubleshoot Performance Issues

### High CPU and/or Memory Usage

What we’re looking for here is what tasks in the COMMAND column are using the most %CPU and %MEM. Once we know this, we can begin further diagnosis.

For example, if you’re seeing high PHP usage, it’s possible your server is experiencing a brute-force attack. High MySQL may indicate database table locking or lack of proper caching.

There are a few different top commands that can come in handy for diving deeper into issues.

 

###### 1. Show the full path of your processes

To view the entire file path of your processes, press “c” while top is running.

###### 2. Display the processes of a specific USER

If you’ve identified one of your websites or would like to take a deeper look into users like Redis and MySQL, you can view their processes by exiting top, and then running:

```
top -u {username}
```

Example:

```
top -u mysql
```

###### 3. Change the screen reset interval

If information is moving too fast, you can change the delay by pressing “d” inside of top and entering the number of seconds you’d like to set refresh intervals and then pressing enter. The default refresh interval is 3 seconds.

###### 4. Kill a process

If you need to kill a process without exiting top, press “k” and then type the PID number and hit enter.

###### 5. Re-order by highest CPU usage

If you need to reset the order of commands to list them by highest CPU usage first, press “SHIFT+P“.

 

### Steal

First, are you experiencing sustained steal? If yes, you need to contact your IaaS provider (DigitalOcean, Linode, Vultr, etc) and inform them of the problem so they can take action accordingly.

 

### I/O Wait

Second, are you experiencing high iowait? If this is high, then the CPU is waiting on the IO/drives. You can exit top and install and run iotop to see which process is causing the most I/O utilization on your server.

To exit top hit Ctrl+C.

You can install iotop with:

```
apt install iotop
```

Then run:

```
iotop
```

iotop will list all of the processes running, with the heaviest process at the very top.

To exit topor iotop hit Ctrl+C.

 

## Further Reading

htop is better for pinpointing the direct cause so that you can dig deeper into any specific process issues you come across. Learn more about htop and further troubleshooting in the following guides:

You may also want to check out the Security and Performance sections of our knowledgebase here:

You can also learn more about top directly on your server with:

```
man top
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

