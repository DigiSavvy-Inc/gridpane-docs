# How to Configure Git Repositories for GridPane Hosted Websites | GridPane

# How to Configure Git Repositories for GridPane Hosted Websites

 

20 min read 

### Table of Contents

 

## Introduction

In this article, we’ll look at how to set up your WordPress website Git repositories (repos) to work correctly with the GridPane platform.

Public vs Private Repos: Both public and private repos will work with GridPane. Using public repos is a simple process – all you need is the public URL, and you’re all set. Private repos require more initial set up and this will be the main focus of this article.

This isn’t a “how to use Git” article and assumes you know how to create and work with Git repositories. This is a guide to help you correctly configure your repos.

 

 

### OpenLiteSpeed & Git

OpenLiteSpeed is currently not available for our Git integration or Multitenancy.

 

### Information

Before you begin, please be sure to read this article on the two different types of integrations available and how they are configured:
An Overview of GridPane Git Options: Full and Hybrid Repo Types

Part 1: Setting Up Your Repositories

 

## Download GridPane’s Base Full and Hybrid Repositories

Before you attach a repository to GridPane, you need to first make sure that your file structure is set up correctly. To assist with this, we’ve created three base repo’s that you can fork and use to create your own repos – these repos are automatically kept up to date with the latest WordPress version. Learn more about repo types here.

 

 

### Important

The repositories linked below contain a file called main.yml inside the .github/workflows directory. This file is used to keep our repo's up-to-date with the latest version of WordPress for you to fork/download. Please remove this file from your own repository or it will replace your codebase with the latest version of WordPress.

### 1. Full Repository: All GridPane Plugins

This repo contains all of our mu-plugins, which include wpFail2Ban, our SSO plugin, caching plugins, etc. This is an example of a properly configured repo for a site with all our app settings enabled that require these plugins.

You can view/fork/download the full repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-template-all-pluginsBranch: main

### 2. Full Repository: Basic

This repo is essentially an empty repo with only what you need to begin using our Git integration. You can view/fork/download the full repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-templateBranch: main

### 3. Hybrid Repository

You can view/fork/download the hybrid repository here:

https://github.com/GridPane-Dev/gridpane-wordpress-hybrid-templateBranch: main

### Additional Info

Each of the repos contains extensive README.md files on how to work with these repos and our Git integration.

 

## The .gpconfig Directory

Once a website has been converted into a Git site, both full and hybrid types have a GridPane directory inside /htdocs called: .gpconfig.

This directory will contain a max of either 5 or 6 files depending on whether it’s a full or hybrid deployment:

```
.gpconfig/hybrid
.gpconfig/keep.releases.gpconfig/predeploy-server.sh
.gpconfig/predeploy.sh
.gpconfig/postdeploy.sh
.gpconfig/postdeploy-server.sh
```

The hybrid file won’t be present in full repositories.

 

## Setting Your Repository Type

The presence of the hybrid file will determine the type of deployment that we run:

This is all set up directly inside your Git repo. 

## Pre and Post Deployment Scripts

Inside our repo downloads above you will find the following four empty scripts:

```
.gpconfig/predeploy-server.sh
.gpconfig/predeploy.sh
.gpconfig/postdeploy.sh
.gpconfig/postdeploy-server.sh
```

These scripts will execute in the above order. If any of the bash scripts return a non-0 response then the deployment will fail.

The -server.sh scripts are run as root, with the others running as the site system user. All are run from the /.gpconfig directory.

### Scripts that run as the root user

The following are run as root:

```
.gpconfig/predeploy-server.sh.gpconfig/postdeploy-server.sh
```

The root scripts can be useful for running scripts across the server and microservices which need elevated privileges (be careful and test in a non-production environment when creating your scripts).

### Scripts that run as the system user

The following are run as the website system user:

```
.gpconfig/predeploy.sh.gpconfig/postdeploy.sh
```

These system user scripts can be useful for running system user functionality, PHP, WP-CLI, etc.

Remember to add the correct path to WordPress core files for WP-CLI commands, in the case of a full deployment this would be the directory above.

 

## The keep.releases File and Release Directory Retention

```
.gpconfig/keep.releases
```

The contents of this file can be an integer only, and the integer must be greater than or equal to 3. This represents the minimum number of releases we will allow you to retain.

This integer is the number of releases that the system will retain in the following directory:

```
/var/www/{site.domain}/releases
```

Please see below for details of the releases and release directory naming convention.

 

## The wp-config.php File and Your Git Repositories

Our base templates (linked to above) will make getting started creating your repo’s a simple process.

However, as with regular sites at GridPane, don’t include a wp-config.php file in your repositories. We store the wp-config.php (and our user-configs.php) one level up from the /htdocs directory, and a competing wp-config.php can cause strange behavior and break your sites. Learn more here:

Working with the wp-config.php on GridPane and an introduction to user-configs.php

When developing locally, if your WordPress setup includes wp-config.php in the main WordPress directory, you can use the .gitignore not to track this file with Git.

 

## GridPane Plugins and Full Repos

The following only applies to Full repositories, not Hybrid repositories.

This base repo is an example of a repo configured for full deployment (all WordPress core files, plugins, and themes managed by Git repo), with all of the requisite plugins required for the following GridPane panel functionality:

The three sections below cover caching, WPFail2Ban, and GridPane must-use plugins.

 

### Caching Plugins

If you’re using our server caching then you should include our caching plugins.

These would be required based on the site’s GridPane App configuration of:

```
wp-content/plugins/gridpane-redis-object-cache
wp-content/plugins/nginx-helper
wp-content/object-cache.php <-- drop in from gridpane-redis-object-cache
```

If you are using the Nginx Stack and Nginx Page Caching and Redis Object Caching you will need to use these plugins:

These can be found directly inside this template Git repo: GridPane WordPress Template All Plugins

If you are using Nginx FastCGI caching, you will also need the GridPane Nginx-Helper Helper. This is not needed for Redis-based Page Caching.

GridPane Nginx Cache Purger (GridPane-Dev GitHub Page)

 

### WPFail2Ban

If your site is using the WPFail2Ban integration in the Panel, then you will need this plugin too. On Deploy, we detect if this plugin exists and if your site is configured for it, and look after the symlinking to MU.

WPFail2Ban (WordPress.org download link)

 

### Must-Use Plugins

After a deployment, a function runs and checks for all of the plugins needed for their corresponding functions to work, and it will sync the state to the app.

This means that the site itself is the source of truth.

If anything is missing (apart from the login server) we will just adjust the app data to match, which will display these settings as either toggled on or off accordingly.

These would be required based on the websites GridPane App configuration of:

#### MU Plugin Links

If your site is using the GridPane Sendgrid Mailer integration, then you will need to include that plugin as an MU-Plugin. The repo linked here has instructions, but you can check the mu-plugins directory of this repo to confirm the correct configuration.

GridPane Mailer (GridPane-Dev GitHub Page)

If your site is using any of the GridPane Additional Security Beta settings, then you will need the appropriate MU-Plugin for that feature. The repo’s linked here have instructions, but you can check the mu-plugins directory of this repo to conform correct configuration.

All sites require the wp-cli-login-server.php mu-plugin for SSO to function. If this is not found we will install it on SSO if possible, but it might make sense just to include it in your repo and control its update too.

WP-CLI login server (aaemnnosttv Github)

 

## Plugins and Hybrid Repos

Any plugins that you include in:

```
wp-content/plugins
```

Will be deployed to the releases directory, and then rsynced to the htdocs/wp-content/plugins directory with delete flag to overwrite any existing matching plugin.

### Must-Use (MU) Plugins

Any must-use plugins that you include in:

```
wp-content/mu-plugin
```

Will be deployed to the releases directory, and then rsynced to the htdocs/wp-content/mu-plugin directory with delete flag to overwrite any existing matching mu-plugin.

 

Part 2: Public vs Private Repositories

 

## Using Public Repositories

Using public repositories is simple. Once your repo has been created and added to your chosen Git host (GitHub, GitLab, Bitbucket, etc), all you need to do is copy your repo URL and then you’re ready to start using Git with GridPane – see the previous section for details.

If you’re using freely available themes and plugins then a public repo is fine for this use case.

To get started, please see this article:

Using the GridPane Git Integration

 

## Using Private Repositories with Tokens

Using private repos requires more initial setup than using public repos. This can be done with either Personal Access Tokens or SSH Keys.

Below we’ll take a look using personal access tokens with Github as the example. In the near future, we’ll update the article for using private repos with SSH keys.

 

## GitHub Personal Access Tokens

GitHub’s access tokens aren’t ideal as they apply to an entire account, and there isn’t an option to create an individual token that’s specific to a single repo. However, there is scope for them, and this can still be an acceptable setup for most use cases.

In GitHub from your account dropdown and go to: Settings > Developer Settings > Personal Access Tokens:

Click Generate new token:

Here we need to:

Next, scroll down to the bottom and click the Generate Token button.

You’ll be taken to a new page and presented with your token. Click the copy icon.

Now you can use that key to create the URL for the repo to add, like so:

```
https://{token}:x-oauth-basic@{repo.domain}/path/to/repo
```

For example:

```
https://ghp_iLo3jxeUAMavH7y4xsfmoer349224SQh0pofg1:x-oauth-basic@github.com/gridpane/private-gridpane-wordpress-template
```

This is the URL that you will add to the Git Repository URL field when creating a new repo:

Your private repo is now ready to use with GridPane. To get started using your repo with GridPane, please see this article:Using the GridPane Git Integration

 

## GitLab Deploy Tokens

GitLab allows for individual tokens per repo, which is great.

Navigate to your GitLab hosted repo and go to: Settings > Repository > Deploy Tokens.

Here, enter a name (token name) and a username, select the appropriate permissions (read is necessary, write is optional), and click create. Do not set the expiration date (since a new token would need a new repo connection in the app).

Once configured, click the Create deploy token button.

GitLab will show you your token one time, and never again, so be sure to copy it down.

### Add Your Repo to GridPane

You can use the token username and the token to create the string that you enter in the app as your URL:

```
https://{token.username}:{token}@{repo.domain}/path/to/repo
```

For example:

```
https://gl-deploy-token:[[email protected]](https://gridpane.com/cdn-cgi/l/email-protection)/gridpane/gridpane-wordpress-template
```

Your private repo is now ready to use with GridPane. To get started using your repo with GridPane, please see this article:Using the GridPane Git Integration

 

## Using Private Repositories with SSH Keys

SSH keys would technically be the most secure option for your private repos, though tokens as detailed above will work fine for most use cases. Below we’ll take a look at how to connect to GitHub, GitLab, and Bitbucket Cloud repos using SSH keys.

To do this, we’ll need to generate and then configure a new SSH key pair.  This requires connecting to your servers – if this is your first time doing so, please see the following guides to get started:

 

 

### Information

Please note that it is not possible to directly convert a public github repository to a private one.

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Create and Configure a New SSH Key Pair: Full & Hybrid Git Repositories

The following steps apply to both GitHub and GitLab, with sections specific to each as we go.

The {system.user} referred to in the steps below is your website system user:

### Step 1. Generate System User SSH to use for Git access

Build a site on your server, it will have its user, we will need to create an SSH key for that user:

```
ssh-keygen
```

It will ask you where to add the key, enter the correct file path for an SSH key in the sites system user path:

```
/home/{system.user}/.ssh/id_rsa
```

For example:

```
root@myserver:~# ssh-keygenGenerating public/private rsa key pair.Enter file in which to save the key (/root/.ssh/id_rsa): /home/mysystemuser2424/.ssh/id_rsaEnter passphrase (empty for no passphrase):Enter same passphrase again:Your identification has been saved in /home/mysystemuser/.ssh/id_rsa.Your public key has been saved in /home/mysystemuser/.ssh/id_rsa.pub.The key fingerprint is:SHA256:d1W+dc5Dg9Rwjiof389tyj40rgk3wojfkrxfhQ2W+j85c root@jun15-rep-jeff-do20The key's randomart image is:+---[RSA 2048]----+| =oOoo ..o. .|| + Bo*... oo.+ || . . *o....=.=o+|| . + .= @.o=|| . S + * .oo|| + . .|| o . || . E || . |+----[SHA256]-----+root@myserver:~#
```

 

### Step 2. System User SSH config to use

Next, we need to create a config for this system user, and for the Git SSH user.

Run the following, replacing {system.user} with your websites system user:

```
nano /home/{system.user}/.ssh/config
```

For example:

```
nano /home/mysystemuser2424/.ssh/config
```

In that config file we need to add our config – this differs between providers, and you can see those details below:

```
Host {git.user}
Hostname {git.repo.domain.hostname}
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
```

Then save the file with CTRL+O followed by Enter. Then exit nano with CTRL+X.

#### Format for GitHub:

```
Host github-mywprepo
 Hostname github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

#### Format for GitLab:

```
Host gitlab-mywprepo
 Hostname gitlab.yourwebsite.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

#### Format for Bitbucket Cloud:

```
Host bitbucket-mywprepo
 Hostname bitbucket.org
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

 

 

### Important

This needs to be added as detailed above, with both the host for the SSH user and the hostname for the domain. Without this exact format, the scripts will fail.

### Step 3. Fix perms

Once steps 1 and 2 are complete you will need to make sure that permissions are set correctly on everything in the system user .ssh directory (again, replace {system.user} with your websites system user):

```
chown -R {system.user}: /home/{system.user}/.ssh/
```

For example:

```
chown -R mysystemuser2424: /home/{system.user}/.ssh/
```

 

## Create and Configure a New SSH Key Pair: Multitenancy Repositories

For multitenancy servers, your Git repo is owned by the root user, and it applies to all of the websites on this server. The setup is similar to system user setup detailed directly above.

### Step 1. Generate a new SSH key pair

First, generate an SSH key with:

```
ssh-keygen
```

It will ask you where to add the key, enter the following file path for an SSH key:

```
/root/.ssh/id_rsa
```

For example:

```
root@myserver:~# ssh-keygenGenerating public/private rsa key pair.Enter file in which to save the key (/root/.ssh/id_rsa):Enter passphrase (empty for no passphrase):Enter same passphrase again:...
```

### Step 2. Create SSH config

Next, generate the config file for the root user with the following command:

```
nano /root/.ssh/config
```

In that config file we need to add our config – this differs between providers, and you can see those details below:

```
Host {git.user}
Hostname {git.repo.domain.hostname}
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa
```

Then save the file with CTRL+O followed by Enter. Then exit nano with CTRL+X.

#### Format for GitHub:

```
Host github-mywprepo
 Hostname github.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

#### Format for GitLab:

```
Host gitlab-mywprepo
 Hostname gitlab.yourwebsite.com
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

#### Format for Bitbucket Cloud:

```
Host bitbucket-mywprepo
 Hostname bitbucket.org
 PreferredAuthentications publickey
 IdentityFile ~/.ssh/id_rsa
```

 

## Private SSH Key Repo URL Format

I’m covering this part in advance of actually adding your SSH key to GitHub and GitLab

When using a private repo with an SSH key you will still need to add a repo URL when you configure things inside of your GridPane account.

With the above 3 steps done you can enter the URLs for your Git repo like so:

```
git@{git.user}:relative/path/to/repo
```

Where the {git.user} is that user from the .ssh/config and the relative/path/to/repo is relative to {git.repo.domain.hostname}.

#### GitHub URL Format

If, as an example, my GitHub repo URL is as follows:https://github.com/ste-bell/mywordpresssite

Then this is how you would configure your repo URL inside GridPane:

```
git@github-mywprepo:ste-bell/mywordpresssite
```

If you’re using a self-hosted GitHub clone, please select the Self Hosted Git option and then select GitHub clone.

#### GitLab URL Format

If, as an example, my GitLab repo URL is as follows:https://gitlab.mywebsite.com/gridpane/mywordpresssite

Then this is how you would configure your repo URL inside GridPane:

```
git@gitlab-mywprepo:gridpane/mywordpresssite
```

If you’re using a self-hosted Gitlab, please select the Self Hosted Git option and then select Gitlab Community Edition.

#### Bitbucket URL Format

Note: Bitbucket appends the branch to the URI. I’m not sure if there’s a way around this to work with multiple branches inside one GridPane Git repository integration.

If, as an example, my Bitbucket repo URL is as follows:https://bitbucket.org/ste-bell/mywordpresssite/src/main

Then this is how you would configure your repo URL inside GridPane:

```
git@bitbucket-mywprepo:ste-bell/mywordpresssite/src/main/
```

If you’re using a self-hosted Bitbucket server, please select the Self Hosted Git option and then select Bitbucket Server.

 

## Copy Your Public Key

Finally, before we head over to our Git host, we need to copy the public SSH so we can add it to our repo. You can view the key with:

```
cat /home/{system.user}/.ssh/id_rsa.pub
```

For example:

```
cat /home/mysystemuser2424/.ssh/id_rsa.pub
```

Depending on your terminal settings, you can copy it by simply highlighting it. Otherwise, you should be able to right-click and choose copy if you have it set it up that way.

Now that all the GridPane side of things is done, we just need to add our new SSH key to our Git host website repo.

 

## Add SSH Key to GitHub Repo

Head over to your GitHub account and open the repo that you want to add your SSH key to.

Here choose Settings > Deploy Keys. Click the Add deploy key button and you’ll then be able to add your public SSH key and give it a name:

You may want to name this in a way that it’s easy to connect it to your specific website and its current server name/IP address for easy reference in the future.

You don’t need to allow write access.

Click the Add key button when ready. You’ll then see your key listed and with any other keys you may have and you can also delete it from here as well.

You can now use this repo with your GridPane account.

 

## Add SSH Key to GitLab Repo

Inside your GitLab account and head to Settings > Repository > Deploy Keys.

Here you can add your public SSH key and give it a name.

You may want to name this in a way that it’s easy to connect it to your specific website and its current server name/IP address for easy reference in the future.

You don’t need to allow write access.

When ready, click the Add key button.

Once added, it will appear alongside any other keys that have access to the repo, and you can revoke access from here in the future when needed.

You can now use this repo with your GridPane account.

 

## Add SSH Key to Bitbucket Cloud Repo

Inside your Bitbucket Cloud account open up your repo and then through to Repository settings > Access Keys.

Click the Add key button:

Here you can add your public SSH key and give it a name.

You may want to name this in a way that it’s easy to connect it to your specific website and its current server name/IP address for easy reference in the future.

You can ignore the sections below the section where you paste in your key. By default, these only allow for read-only access.

Click the Add SSH key button when done.

Once added, it will appear alongside any other keys that have access to the repo, and you can revoke access from here in the future when needed.

You can now use this repo with your GridPane account.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

