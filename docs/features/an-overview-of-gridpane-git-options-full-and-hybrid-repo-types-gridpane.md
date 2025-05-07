# An Overview of GridPane Git Options: Full and Hybrid Repo Types | GridPane

# An Overview of GridPane Git Options: Full and Hybrid Repo Types

 

4 min read 

### Table of Contents

 

 

### OpenLiteSpeed & Git

OpenLiteSpeed is currently not available for our Git integration or Multitenancy.

## Introduction

GridPane now fully supports Git-based websites. There are 2 types of Git integration available:

In this article, we’ll take a look at what these are, how they work, and how this is configured on your server.

 

## Repo Types and Structure

The following details how our full and hybrid options differ, and how they’re configured on the server.

 

### Full Repositories

Our full integration is what most users will be familiar with, and with this WordPress core, plugins, and themes are all managed via Git. The entire codebase is immutable and so WordPress updates can only be made via Git deployments.

 

### Hybrid Repositories

Our hybrid integration is for those of you who only want to handle specific plugins and themes via Git. Unlike the full repo as described above, the hybrid repo is not immutable, so WordPress core and any other themes and plugins not set in your repo are handled the traditional way inside the WordPress dashboard.

 

### Setting Your Repository Type

Once a website has been converted into a Git site, both full and hybrid types have a gp directory inside /htdocs called: .gpconfig.

This directory will contain a max of either 5 or 6 files depending on whether it’s a full or hybrid deployment:

```
.gpconfig/keep.releases
.gpconfig/hybrid
.gpconfig/predeploy-server.sh
.gpconfig/predeploy.sh
.gpconfig/postdeploy.sh
.gpconfig/postdeploy-server.sh
```

The presence of the hybrid file will determine the type of deployment that we run:

This is all set up directly inside your Git repo.

### Deployment Scripts

The other .sh files handle deployments.

```
.gpconfig/predeploy-server.sh
.gpconfig/predeploy.sh
```

These are bash scripts that will run prior to the Git pull. If the bash scripts return any non-0 response then the deployment will fail.

```
.gpconfig/postdeploy-server.sh
.gpconfig/postdeploy.sh
```

These are bash scripts that will run after the Git pull. If the bash scripts return any non-0 response then the deployment will fail.

More details about these and the keep.releases file can be found in this article:

How to Configure Git Repositories for GridPane Hosted Websites

 

## Full Repositories and their Deployments

This type of repo has the entire WP site in the directory.

Updates to WP core, plugins, and themes are all handled via the repo.

You and your clients will not be able to update core, plugins, or themes via the wp-admin. This is made immutable.

### Directory structure changes

With this type of deployment we pull the contents of the repo into a release directory and make the site /htdocs a symlink to that directory:

```
/var/www/site.url/htdocs ->. /var/www/site.url/releases-{timestamp}
```

For example:

```
root@myserver:# ls -la /var/www/test.sitetotal 48drwxr-xr-x+ 9 test19461 test19461 4096 Jun 16 12:32 .drwxr-xr-x+ 6 root root 4096 Jun 16 11:12 ..drwxr--r-- 3 root root 4096 Jun 16 11:22 .duplicacydrwxr-xr-x 2 test19461 test19461 4096 Jun 16 11:12 dnslrwxrwxrwx 1 root root 46 Jun 16 12:32 htdocs -> /var/www/test.site/releases/release-1655382717
```

We also create a public directory at /var/www/site.url/public and we make the wp-content/uploads directory a symlink from that:

```
/var/www/site.url/htdocs/wp-content/uploads -> /var/www/site.url/public
```

For example:

```
root@myserver:~# ls -la /var/www/test.site/htdocs/wp-content/total 20drwxr-xr-x 4 test19461 test19461 4096 Jun 16 12:32 .drwxr-xr-x 8 test19461 test19461 4096 Jun 16 12:32 ..-rw-r--r-- 1 test19461 test19461 28 Jun 16 12:32 index.phpdrwxr-xr-x 3 test19461 test19461 4096 Jun 16 12:32 pluginsdrwxr-xr-x 5 test19461 test19461 4096 Jun 16 12:32 themeslrwxrwxrwx 1 root root 25 Jun 16 12:32 uploads -> /var/www/test.site/public
```

### The Deployment Process

The deployment process runs as follows:

The app will then notify once the deployment is complete. 

## Hybrid Repositories and their Deployments

If this file exists:

```
/var/www/site.url/htdocs/.gpconfig/hybrid
```

Then the scripts run a different process to the one detailed in the previous section.

Sites that are using the hybrid deploy method have no directory changes re symlinks and they are not immutable.

Users who use this method can create repos that contain just their version-controlled plugins and themes, for example:

```
.gpconfig/hybrid.gpconfig/predeploy-server.sh.gpconfig/predeploy.sh.gpconfig/postdeploy.sh.gpconfig/postdeploy-server.shwp-content/my-pluginwp-content/my-plugin/my-plugin.php
```

The process is as follows:

If all processes return 0 then we rsync all the directories contained within to their matching place in /htdocs.

If any of the steps return a non-0 response we error out and we don’t run the rsync.

The app will then notify once the deployment is complete.

### Additional Notes

With this method there is a duplication – a version of the plugins is stored both in htdocs and in the release directory.

However, this method allows for you to version control any custom plugins and themes, and still run updates on other plugins from within wp-admin because the rest of your website isn’t modified at all.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

