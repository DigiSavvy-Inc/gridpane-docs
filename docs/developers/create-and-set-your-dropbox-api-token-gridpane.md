# Create and Set Your Dropbox API Token | GridPane

# Create and Set Your Dropbox API Token

 

3 min read 

 

### Important Dropbox Update

12/04/2022
Dropbox has updated their API so that it's no longer possible to generate tokens without an expiry time. Due to this extremely unfortunate and disappointing development, it means we can no longer support Dropbox as a remote backup option for the foreseeable future unless they undo this change. 

Dropbox has repeatedly made API changes over the past 2 years that have caused numerous issues for it's integration and development for our V2 backups system. Please consider one of the other three alternatives that we integrate with for your remote backups.

## Alternative Remote Provider Options

The following articles detail how to get started with the three other remote providers we integrate with:

 

## Further Reading

For further information about how backup systems work, the available options for configuring them, and for setting up remote backups (available on V2), please see the articles listed below.

### Strategy

Recommended Backup Strategy

### V2 Backup Documentation

 

## Introduction

Dropbox is a solid and reliable storage provider and this article assumes that you already have a Dropbox account.

Somewhat unfortunate timing, Dropbox has released a new version of their API as we’ve been developing our backup system. For the moment, our system works with the legacy API.

There are two methods detailed below for generating an API token that will work with GridPane.

 

## Step 1. Create Your Dropbox API Token

Below outlines 2 different methods for generating your API token. You can choose either.

 

### Method 1. Quickly Create Your Key via Duplicacy.com

Head to https://duplicacy.com/dropbox_start.html and click the Continue to get started:

You’ll be taken to Dropbox to authorize Duplicacy to create its own folder (Apps > Duplicacy). Click the Allow button to continue:

Here you’ll be presented with your API token that you can add to your GridPane account:

Copy the token and proceed to Step 2 below.

 

### Method 2. Create Your Token Within Dropbox

To begin, first sign in to your dropbox account and then head over to Dropbox App Console here: https://www.dropbox.com/developers/apps

Here there’s a small blue Create App button. Go ahead and click on this to create a new app.

Here you need to select: –

And then click the blue Create App button.

You will automatically be taken to your apps management page. Here, first click through to the permissions tab and give your API the correct permissions and click the Submit button:

Once selected, click back to the Settings tab and scroll down approximately halfway to the “Oauth” section.

Here you’ll see the option to generate an access token – “Generated access token” followed by a button labeled “Generate“, and also the “Access token expiration” dropdown.

Set the expiration to “No Expiration“.

Next, click the Generate button and your API token will be displayed. Copy it and then head over to your GridPane account.

IMPORTANT: On very rare occasions Dropbox will create a token that begins with a dash “-“, e.g:

```
-od2UzsdgfGGGSDfewfregg8gLLLLq_FAWS5wtAnmHLvZa6QZLq99RkblsDD0qub
```

If this happens, please refresh the page and hit the generate button again as the “-” will be read as a flag on the server and will result in an error.

 

## Step 2. Add your Dropbox API Token to GridPane

Back in your GridPane account, click through to your settings page:

Here, click through to the Integrations page, click Backup Providers, and then Dropbox:

Give your key a name, enter your API token, and click the Create button.

You’re all set!

To learn how to configure remote backups for your websites check out the following article for a full walk-through:

Remote Website Backups

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

