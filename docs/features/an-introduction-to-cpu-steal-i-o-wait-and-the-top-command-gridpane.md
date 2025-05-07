# An Introduction to CPU Steal, I/O wait and the top command | GridPane

# An Introduction to CPU Steal, I/O wait and the top command

 

3 min read 

### Table of Contents

 

## Introduction

CPU steal can be highly problematic. Fortunately it’s not common place on the providers we integrate with, but we do see this from time to time, and you may have seen us mention “noisy neighbours” in the Facebook group or directly on support. In this article we’ll give you a brief overview of what CPU steal is, and also give you a quick intro to the top command.

 

## What is CPU steal?

In a nutshell, CPU steal is CPU time that is stolen from a VPS by the hypervisor (AKA the virtual machine monitor / VMM).

Your VPS shares resources with other instances that also exist on the same server and CPU cycles are one of those shared resources. Unlike RAM, which has a specific, set limitation, CPU is more flexible. CPU cycles are shared across other instances that exist on the same server.

For example, if your VPS was one of 10 equally sized instances on one server, its CPU isn’t capped at 10%. You could potentially go above your allocation and steal from other instances on your server, and the same is true for them having the potential to steal from you.

If your VPS displays a high %s in top, this means CPU cycles are being taken away from you by other instances/hypervisor processes (more info in the next section). The more steal you experience, the more your servers performance will suffer.

### CPU steal value

CPU steal is measured in percentage – 0% being no steal, 100% being all of your cores being 100% used.

### When is CPU steal problematic?

You’ll see small amounts of steal, and less than 10% is generally nothing to be concerned about unless is for a prolonged period.

Consistently high steal for a prolonged period can cause significant performance issues for your server processes and websites. Above 20% can be problematic.

### Next steps if you experience high CPU steal

If you’re experiencing server steal then you need to contact you IaaS provider directly to let them know what’s going on so they can take action accordingly.

If they’re unable (or unwilling) to solve the problem, you may need to move your site/s to a new server to ensure better, more reliable performance.

 

## What is I/O wait?

Far less prominent than CPU steal is I/O wait time. This is where your CPU is idle because there are no tasks ready to run, and it’s waiting on I/O. We rarely see it, but it’s good to know.

The following is copied and pasted from the sar manpage:

%iowait: Percentage of time that the CPU or CPUs were idle during which the system had an outstanding disk I/O request.

I/O wait is simply idle time where no tasks could be scheduled.

 

## Running the top command

For this you’ll need to SSH into your server. Please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Checking for CPU steal with top

The top command will let you know if other VPS’s on your server are stealing your CPU usage, or if your CPU is waiting on IO/drives. Run:

```
top
```

And you’ll see a table appear that looks as follows. We’re interested in the parts highlighted in red:

Steal “st”Here you can see there’s no steal, but sometimes neighbours on your server can potentially steal a lot of your CPU – sometimes over 50% or more.

I/O Wait “wa”If this is high then the CPU is waiting on the IO/drives. You can exit top and install run iotop to see which process is causing the most I/O utilization on your server.

To exit top hit Ctrl+C.

You can install iotop with:

```
apt install iotop
```

Then run:

```
iotop
```

iotop will list all of the processes running with the heaviest process at the very top.

To exit top/iotop hit Ctrl+C.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

