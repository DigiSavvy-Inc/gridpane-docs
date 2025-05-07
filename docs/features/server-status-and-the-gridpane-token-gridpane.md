# Server Status and the GridPane Token | GridPane

# Server Status and the GridPane Token

 

4 min read 

## The GridPane Token

The GridPane token is our API token and it allows your servers to talk to GridPane, and allows us to do all the things we need to do to ensure your stack stays up-to-date.

## Server Status and Scripts

On the servers page in your account, the status of each of your servers will be displayed with a refresh icon alongside it.

On clicking you’ll see the following:

And if you hover over it will tell you the last time the server was synced by the app:

This refresh icon will do a couple of things: –

 

## There are 3 different Server States

### 1. Active – Green dot and green bar

If your server is an API server then GridPane is connected, can SSH, and the API can see the server at the IaaS provider.

If it’s a custom server then GridPane is connected to server and can SSH.

All green mean’s all is well.

### 2. Active – Orange dot and green bar

Your server and your websites are fine, please don’t panic!

This simply means that we will not be able to delete or rename the server at your API provider. GridPane can SSH in and run commands, and you can still manage your websites from within the dashboard.

This status will only ever show for API providers and it specifically means there is no API connectivity at the IaaS provider. This could mean either a mismatching token or missing token, or that your API key needs to be refreshed at your IaaS provider.

Again, this is a very minor issue. Please just take care to delete your server directly at your provider should you delete it in the future.

### 3. Disconnected – red dot and red bar

This means there is no SSH access and we can’t log in to the server. It may also mean the IaaS API key is missing.

 

## Status = Active, Orange Dot

This generally means one of of the following things: –

### 1. You need to whitelist our IP addresses

This is common for DigitalOcean and Vultr, but can be necessary at other providers too. Please see this article for details:

Whitelisting GridPane at Your Server Provider

### 2. Your API key has been switched out

You’ve changed the API key from one account to an API key from a different account. Now that the original accounts API key is unavailable, we can’t connect to your server.

 

## Status = Disconnected

This generally means one of of the following things: –

### 1. You need to whitelist our IP addresses

As above, this is common for DigitalOcean and Vultr, but can be necessary at other providers too. Please see this article for details:

Whitelisting GridPane at Your Server Provider

### 2. Your server is on the old PLAID Stack

You’re running our old PLAID stack on Ubuntu 16.04, and this is incompatible with our latest scripts and updates. If your server is on our PLAID stack then we highly recommend that you migrate your websites to a new, up-to-date server running our Prometheus stack on Ubuntu 18.04.

### 3. Your Server has been Renamed

You’ve renamed your server directly at your IaaS provider. Here you can rename your server back to its original name at your provider and then try to re-sync again inside of GridPane.

### 4. Your GridPane Token needs a refresh

Your GridPane token on that server is out of sync. If you’re on Prometheus and haven’t manually disconnected your server from us or deleted it, try hitting the refresh icon and the app will try to reconnect to your server.

If that doesn’t work, navigate to Settings > GridPane API > GridPane Token and hit refresh. Then head back to your Servers page and try to re-sync.

### 5. Your IaaS Provider API Key needs a refresh

If the above doesn’t re-sync your server back to “Active”, it may need to regenerate your API key at your IaaS provider and switch the old one in your GridPane account out for the newly generated one. Then head to your servers page and hit the sync button again.

### 6. Your Server is down or has been deleted/suspended

Your server has been disconnected from our app, and we can no longer connect to it. This could mean that: –

### 7. Your server doesn’t contain our SSH Key

This one is unlikely, but if the issue isn’t one of the above, then please open a support ticket and let us know the steps you’ve taken. We can then check out the server and add our API key if it’s missing.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

