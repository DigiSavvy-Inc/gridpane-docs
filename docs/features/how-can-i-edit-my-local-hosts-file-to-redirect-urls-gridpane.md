# How can I edit my local hosts file to redirect URLs | GridPane

# How can I edit my local hosts file to redirect URLs

 

5 min read 

### Table of Contents

 

## Introduction

A local hosts redirect is a handy trick to tell your computer to ignore the live A and CNAME records for a website, and instead to visit a different IP address. This is primarily used by the GridPane community during their migrations so they migrate their websites from other hosts directly to the same URL, and then check it over before changing the DNS to point to the new GridPane server.

This technique can be useful for multiple purposes, including:

In this article, we will use a simple example to go through the process of editing your hosts file to enable this.

 

### Alternative Option

You can also accomplish this with tools like https://hosts.cx/. This can be a handy website for your toolbox and potentially sharing with clients, but we highly recommend that you learn how to use your local hosts file for redirects for speed and efficiency.

 

### Example Scenario

In our example, we have a new client who owns their domain at http://an-example.com  and they currently have a coming soon holding page at their old hosting.

We are going to install a development site on a GridPane server and edit our hosts file to redirect our browser to the GridPane server when visiting the client domain.

In our terminal, we can confirm the IP of the server that their domain currently resolves to quite easily by using the ping command.

```
ping an-example.com
```

This command will work for macOS, Windows, and Linux machines.

As we can see, our example clients holding page is currently being hosted on a server with the IP of 104.248.77.241.

Whenever someone on the internet visits their domain, an-example.com , their DNS records point them to this server.

Below is how to set up a local hosts redirect to visit the same URL but on a different IP.

 

## Video Guides

### Windows Walkthrough

 

### Mac Walkthrough

 

## Step 1. Copy GridPane Server IP Address

This guide assumes that you have your server and new WordPress website up and running in your GridPane account.

To copy your IP address, head over to the Sites page inside your account, locate your website, and click on the IP address to copy it.

 

## Step 2. Edit your Hosts file to create the URL redirect

To edit your hosts file manually, simply locate it on your system and open it up in your preferred text editor. The locations for Windows, macOS, and Linux are detailed below.

Alternatively, if you’d prefer to use software that makes it a bit easier to do the same, you may want to use Gas Mask (for Mac) or Hosts File Editor (for Windows).

### Windows

On Windows this is located at:

c:Windows/System32/Drivers/etc/hosts

### MacOS

On macOS this is located at:

/private/etc/hosts

### Linux

On Linux this is located at:

/etc/hosts

Within your hosts file add an entry at the bottom, using the GridPane server IP address you wish to redirect to IP and the live domain you wish to redirect away from. It is usually best to add both the root  domain and the www  host domain.

139.59.190.225 an-example.com139.59.190.225 www.an-example.com

Make sure that there is only one space or tab between the IP address and the domain.

Save your file and exit.

Your local hosts redirect is now set up.

 

## Step 3. Test that your Hosts URL redirect is working

The quickest and easiest way to test your redirect is to open up the website in a brand new incognito window (note that if you’ve already visited the site in an incognito window, your browser will still likely have cached the old IP).

Here, you should see your new WordPress website on your GridPane server. In our example, the website is:

http://an-example.com

 

### Troubleshooting: Still Seeing the Live Website

If you’re still seeing the live website, you can also clear your local machine system cache.

This will force your browsers to visit the new IP address that you’ve set in your redirect. You can follow these instructions to learn how to do this for your operating system:

Alternatively, you can try visiting the website in an entirely different browser, and again using an incognito window.

 

### Troubleshooting: HTTPS Redirects

If you have migrated a website in but you’re unable to access it due to an HTTPS / insecure error, there are a couple of workarounds you can use to fix the issue.

Depending on the cause, you can either:

You can provision an SSL certificate before you change your DNS records to point to the site by following one of these guides:

You may need your client’s assistance if you don’t have access to the domain’s DNS provider.

 

### Test Your Redirect Alternative Method: Ping Website

Now that your cache is cleared, you can retest using ping.

ping an-example.com

If your results show a ping to your GridPane server, then the redirect is working.

In this example, the server I want to redirect to has an IP address of 139.59.190.225. We can see from the ping results to the domain an-example.com is resolving to this IP address, this confirms the redirect is working.

 

## Step 4. Remove the Hosts Redirect when finished

Don’t forget, once you are finished using the hosts redirect, you need to remove it from your hosts file.

This will ensure that you don’t accidentally work or try to troubleshoot issues, etc, on the wrong version of your site.

To remove the redirect, simply open up the hosts file, delete the two lines you’ve added, and then save.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

