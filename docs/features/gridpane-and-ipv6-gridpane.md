# GridPane and IPv6 | GridPane

# GridPane and IPv6

 

2 min read 

## Introduction

GridPane requires that your servers and website’s have an IPv4 address, but for those of you who want to add an IPv6 address for your websites as well, this article is for you.

### Table of Contents

 

## What is IPv6?

IPv6 is the 6th and latest version of the Internet Protocol (IP). It brings a few benefits over IPv4, but most importantly it massively expands the number of possible IP addresses available for the internet as a whole.

Other advantages over IPv4 include multicast support, routing efficiency improvements, and security improvements.

A number of countries, particularly in the EU are pushing for the adoption of IPv6, and you may have clients reach out to you and ask for it to be enabled on their websites. As time goes on it will increasingly become the norm to have both IPv4 and IPv6 records for all websites.

### Will IPv6 Make My Website Faster?

Maybe, but this is generally not going to be a major performance booster for you. It’s also possible it could make your website slower at this point in time, though unlikely.

 

## Setting DNS AAAA Records for IPv6

IPv6 uses AAAA records, and these are only used when a website has an IPv6 is available.

These work exactly the same way that A records work for IPv4, enabling browsers and other devices to lookup an address where they can go to connect to your website.

Here’s an example of what setting records for a regular domain looks like:

 

## IPv6 and GridPane

GridPane’s functions are designed to work with IPv4, so be sure that your server is always set to IPv4 as the primary IP, and that your websites all have both IPv4 as well as IPv6. When doing anything that requires an IP address, we recommend that you use the IPv4 address.

For example, when accessing the site over SFTP, or migrating a site using a plugin like Migrate Guru that will access these details.

Aside from the above, GridPane is IP agnostic and there should be no issues with using AAAA records on your websites. Just make sure you update them as well as your A record/s when moving the site from one server to another.

 

## Further Reading

You can learn more about managing DNS here:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

