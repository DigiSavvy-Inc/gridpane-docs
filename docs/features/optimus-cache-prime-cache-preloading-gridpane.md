# Optimus Cache Prime - Cache Preloading | GridPane

# Optimus Cache Prime – Cache Preloading

 

7 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

Optimus Cache Prime (fantastic name!) is a cache preloader for websites that use an XML sitemap, created by Patrick Mylund Nielsen of https://patrickmn.com/.

This is a particularly useful tool for cache preloading on GridPane, especially once a full site cache clear has been ran via the Self-Help tools.

This article will walk you through how to set this up for your websites and, if you wish, set it up as a cron job.

 

## Part 1. Download Optimus Cache Prime

First, we need to connect to our server via SSH. Please see the following guides to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

We’re now going to download and unzip OCP. As I’m going to be running it as a cron job (part 4), I’m going to store it where the bulk of my other cron jobs run: /usr/local/bin. You’re welcome to install it elsewhere if you wish – it will still work correctly. To begin I’m going:

```
cd /usr/local/bin
```

To download the file we can use the wget command. At the time of writing, this looks as follows:

```
wget https://cdn.pmylund.com/files/tools/ocp2/linux/ocp-2.7-amd64.tar.gz
```

Note – we’re downloading the Linux (64-bit) version.

 

## Part 2. Extract

The file we’ve just downloaded is a tar.gz file, so we’re going to extract the file with the tar -xf command as follows:

```
tar -xf FILENAME.tar.gz
```

For me at the time of writing the command is therefore:

```
tar -xf ocp-2.7-amd64.tar.gz
```

 

## Part 3. Run a preload

You may wish to test this is working correctly on a small test site. First run a full cache clear via the self-help tools like so:

Then, back inside your server, navigate to the ocp directory. I’ve installed it here:

```
cd /usr/local/bin/ocp
```

And then run the following replacing the link below with your actual sitemap link:

```
./ocp https://yourwebsite.com/sitemap_index.xml
```

This will now run and preload your websites cache. You can run this anytime you need to, and you can view the all of the Optimus Cache Prime commands available by entering ./ocp on it’s own while inside the ocp directory.

 

## Part 4. Setup a cronjob (optional)

When setting up a  cron job for Optimus Cache Prime, you may also wish to install the one.sh script by the same author. This is particularly useful for large sites that may take awhile to run, as we can use this to check if a preload is still in progress and abort if so – and you can use this for other cron jobs as well.

### DOWNLOAD AND INSTALL ONE.SH

If you skipped step 3, navigate to the ocp directory with:

```
cd /usr/local/bin/ocp
```

We can download and install using the wget command again. I’ll be downloading and installing this inside the ocp directory as follows:

```
wget https://cdn.pmylund.com/files/tools/one/one.sh
```

### Change the permissions for One.sh

By default one.sh is installed without the permissions it needs to be able to run (execute). We need to change this with the following command:

```
chmod +x /usr/local/bin/ocp/one.sh
```

 

 

### Cronjob NOTE

Below details two ways to set up your cronjob. This will become easier in the future, however for now you may wish to use the cron.d method in 4.2, instead of the crontab as detailed in 4.1. You can learn more about cron.d here: About Cron.d

## Part 4.1 Set the Optimus Prime Cronjob via the Crontab

To setup our cronjob, we need to run:

```
crontab -e
```

You’ll be given a choice of editor. We recommend nano. Hit “1” and then enter.

The crontab looks as follows:

Navigate to the bottom of the file with your down-arrow key and here we can now enter our cron job. I’ve installed OCP in /usr/local/bin/ocp (the executable “ocp” file is in the “ocp” directory), and so the cronjob I’m setting up looks as follows:

```
*/15 * * * * /usr/local/bin/ocp/ocp https://yourwebsite.com/sitemap_index.xml
```

This will run OCP on your website every 15 minutes. Adjust the time as per your needs – check out https://crontab.guru/ for more information about timing your cronjobs.

### SETUP THE ONE.SH CRONJOB

If you wish to also set up the one.sh script as a cronjob you can add the following to your crontab instead of the cronjob above:

```
*/15 * * * * /usr/local/bin/ocp/one.sh /usr/local/bin/ocp/ocp https://yourwebsite.com/sitemap_index.xml
```

### SETTING A LIMIT ON HOW MANY PAGES CAN BE CRAWLED AT ONCE

To prevent potentially using a lot of server resources, you can limit how many pages OCP will preload at a given moment. Somewhere in the 5-10 range may be ideal, but you can test and adjust accordingly. For example, if you wish to set a limit of 10 pages at a time we could adjust the commands as follows:

For running without one.sh:

```
*/15 * * * *  /usr/local/bin/ocp/ocp -c 10 https://yourwebsite.com/sitemap_index.xml
```

With one.sh:

```
*/15 * * * * /usr/local/bin/ocp/one.sh /usr/local/bin/ocp/ocp -c 10 https://yourwebsite.com/sitemap_index.xml
```

### SAVE YOUR NEW CRON JOB AND EXIT

Now that you’ve set your Optimus Cache Prime cronjob up, save the file with CTRL+O and then Enter. Exit with CTRL+X.

You’re all set!

 

## Part 4.2 Set the Optimus Prime Cronjob via Cron.d

Instead of setting your cronjob up via the crontab as detailed above, you may instead want to use /etc/cron.d. You can learn more about this here: About Cron.d. This will ensure that your cronjob persists if something unforeseen ever happens that wipes the crontab (this is very rare, but it has happened).

### Create your cronjob file

The file name must consist solely of upper- and lower-case letters, digits, underscores, and hyphens. This means that they cannot contain any dots.

```
nano /etc/cron.d/optimuscacheprime
```

I’ve installed OCP in /usr/local/bin/ocp (the executable “ocp” file is in the “ocp” directory), and so the cronjob I’m setting up looks as follows:

```
*/15 * * * * root /usr/local/bin/ocp/ocp https://yourwebsite.com/sitemap_index.xml
```

NOTE: The “root” user after the timing settings is necessary when running cronjobs from cron.d.

This will run OCP on your website every 15 minutes. Adjust the time as per your needs – check out https://crontab.guru/ for more information about timing your cronjobs.

### SETUP THE ONE.SH CRONJOB

If you wish to also set up the one.sh script as a cronjob you can add the following to your crontab instead of the cronjob above:

```
*/15 * * * * root /usr/local/bin/ocp/one.sh /usr/local/bin/ocp/ocp https://yourwebsite.com/sitemap_index.xml
```

### SETTING A LIMIT ON HOW MANY PAGES CAN BE CRAWLED AT ONCE

To prevent potentially using a lot of server resources, you can limit how many pages OCP will preload at a given moment. Somewhere in the 5-10 range may be ideal, but you can test and adjust accordingly. For example, if you wish to set a limit of 10 pages at a time we could adjust the commands as follows:

For running without one.sh:

```
*/15 * * * * root /usr/local/bin/ocp/ocp -c 10 https://yourwebsite.com/sitemap_index.xml
```

With one.sh:

```
*/15 * * * * root /usr/local/bin/ocp/one.sh /usr/local/bin/ocp/ocp -c 10 https://yourwebsite.com/sitemap_index.xml
```

### SAVE YOUR NEW CRON JOB AND EXIT

Now that you’ve set your Optimus Cache Prime cronjob up, save the file with CTRL+O and then Enter. Exit with CTRL+X.

You’re all set!

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

