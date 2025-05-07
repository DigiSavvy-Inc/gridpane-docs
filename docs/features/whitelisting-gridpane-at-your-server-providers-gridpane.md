# Whitelisting GridPane at Your Server Providers | GridPane

# Whitelisting GridPane at Your Server Providers

 

2 min read 

## Introduction

To ensure that our application can connect to your servers, you may need to whitelist our IP addresses. This is especially true for providers that use a firewall or strict API access controls.

### Server Status

If our application can’t connect to your server, you will see a notice on your account Server page that says “Disconnected” along with a red dot (see the Important box below for more info). If we can’t connect via API, you may see “Connected” with an orange dot – this one is nothing to worry about, it just means we can’t delete the server at the provider from within your GridPane account.

### Failover

Also, if you’re using our Failover system, we’ve seen one provider (Genesis Hosting) have an overly zealous firewall, and they have not only banned our application IP address, but they also banned the Failover setup source server IPs from accessing the destination server, thus causing syncing between the two servers to fail.

 

## Whitelist Our IP Addresses

To whitelist us, head to your firewall setup and add the following three IP addresses to your whitelist: 35.199.11.215, 130.211.115.235, and 35.245.53.150.

## DigitalOcean and Vultr

Once you’ve added your API keys to GridPane, creating new servers should generally work correctly out of the box.

If, however, you’ve set up a cloud firewall at either DigitalOcean or Vultr, you may need to whitelist our IP addresses in order to spin up a server.

Please check out the following articles from each provider for more information regarding their firewalls.

### DigitalOcean

https://www.digitalocean.com/docs/networking/firewalls/how-to/

### Vultr

https://docs.vultr.com/vultr-firewall

At Vultr, you’ll also have to add the IPs under the API Access Control as well which you can find here: https://my.vultr.com/settings/#settingsapi

 

 

### IMPORTANT

This is important to ensure that our application can communicate with your servers and your provider. It can also affect your server status on your Servers page within your account. You can learn more about what the different server-status colors mean and how to troubleshoot them in this knowledge base article: 
Server Status and the GridPane Token

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

