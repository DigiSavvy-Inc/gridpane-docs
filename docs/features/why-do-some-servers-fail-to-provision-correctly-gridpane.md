# Why do some servers fail to provision correctly? | GridPane

# Why do some servers fail to provision correctly?

 

2 min read 

### Table of Contents

 

## Introduction

Unfortunately not every server that’s created get’s successfully provisioned. Almost all API servers do, and so do almost all custom VPS provisions when everything is setup correctly, but even then sometimes things fail. Below outlines why this happens.

 

## Failed at 10%

If your server only made it to 10%, that means our app couldn’t connect to your server.

If it was an API server, then this may mean that the data center at the time was down you tried to create your VPS.

If it’s a custom server, then it could be the data center was down, but it’s more likely to be an issue with a closed port, incorrect Ubuntu installation, provisioning code not ran via the root user, or potentially many other different reasons.

 

## Failed at 25%

If your server made it to 25%, then it failed to connect to the Nginx repo, or it got cut off part way through and was unable to complete the installation. If you hover over the provisioning bar, you’ll get a tooltip:

 

## Failed at 50%

In most cases, this means that the server failed to connect to the Percona repo and has not been able to complete the installation.

In much rarer circumstances, a build script right at the beginning may have failed, and the install just hangs. In this case, the bar still may make it to 50%, but there won’t be a tooltip if you hover over it.

 

## Failed at 90%

Failing at 90% means the server has failed to connect to the PHPMyAdmin repo.

 

## Next Steps

If you’re provisioning a server over API, we’d recommend you delete this failed server and spin up a new one.

If you’re using a custom server and it failed at either 10% or 50%-no tooltip, then please check out the article below and make sure you have all the correct settings and Full Ubuntu 20.04 installed and try again.

How to Provision a Custom Server – A General Guide

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

