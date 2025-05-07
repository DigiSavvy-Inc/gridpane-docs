# GridPane V1 (Legacy) Local Backups | GridPane

# GridPane V1 (Legacy) Local Backups

 

15 min read 

 

### V1 Backups End of Life (EOL)

The V1 backups system reached it's supported end of life on December 17th 2021. This does not mean that your V1 backups will stop working or that you will be forced to upgrade to V2, however, you will now need to fix any issues that occur with the V1 system by following the procedures laid out in this article. Our support team will no longer be able to assist with such issues, and our official recommendation is that you upgrade to the new V2 system.

 

### IMPORTANT

Local backups are an excellent tool for quick recovery on a site where a client or core/theme/plugin updates may have made broken things, or you've accidentally deleted the wrong website, etc. However, they should not be your only backup source for disaster recovery. Please see this article for our recommendations:
Recommended Backup Strategy

### Table of Contents

 

## Introduction

The V1 backups system runs on a program called “Borg”. It was our first WordPress website backup implementation and has now been replaced with the much improved V2 system.

All new servers as of November 1st 2021, all new server builds run the new backups system. For servers provisioned before this time still running the older system, please transition as soon as possible – the End of Life for V1 is December 17th 2021. Learn more about how to transition here:

Transitioning from V1 Backups to V2 Backups

 

## Local Backups

Every GridPane server features a Local backups function. You can easily enable it by for every new site added via the GridPane dashboard.

Backups are run every hour on the hour 24/7. The local backups system stores an hourly backup for the past 12 hours, a daily backup for the past 7 days, a weekly backup for the past 4 weeks and a monthly backup for the past 3 months.

But because the backups are deduplicated, this time machine style backup is incredibly efficient with space.

### Limitations

The V1 backup system doesn’t include remote backups to third-party storage. These are stored directly on your server, so if your server was to ever go down, these backups would not be accessible until the server came back online.

Please ensure you also have third party backups for disaster recovery.

### Excluded File Types

There are a few file types that are not backed up with the V1 Borg system.  One, in particular, you should be aware of is .zip files. Please ensure that you have a recovery plan in place for any of these file types if you host them within your websites. Alternatively, consider offloading them to an external system.

.img, .iso, .wpress, .tar, .zip, and .gz file types are excluded:

```
--exclude '*.img' \--exclude '*.iso' \--exclude '*.wpress' \--exclude '*.tar' \--exclude '*.zip' \--exclude '*.gz'
```

The above file formats, particularly .wpress, .zip, and .gz are the common extensions used by backup plugins such as All in One WP Migration. This precautionary measure ensures that your servers are not filled up with backups of other backups, and also ensures that your local backups continue to have enough space to run without either filling up the server or failing due to insufficient disk space.

 

## Remote Backups

Remote backups are available as a part of our V2 backups system. You can learn more about this here:

Remote Website Backups 2.0

 

## Manually Run a V1 Backup Restore

If you need to run a restore and for some reason, you can’t do this directly inside your account, the following is how to run a restore manually over the command line – see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

First, use the following to get a list of the websites available backups:

```
gpbup site.url -get-available-backups
```

This will look something like this:

```
root@servers# gpbup examplewebsite.com -get-available-backupscat: /root/gridenv/backups.system: No such file or directoryIt looks like these commands are being run manually...Command was called locally, we need to pull the GPURL from file...GridPane Developer - Version 1.2.0 ...Validated... running script...GridPane Backup directory is ready...GridPane Backup Databases directory is ready...VirtualEnv Installed...Resistance is Futile...RClone Already Installed...Backup directory /opt/gridpane/backups/snapshots already exists...Current backup version is 1...Work beginningLooking for examplewebsite.com ...Site examplewebsite.com located...Getting available backups for site examplewebsite.com...Checking for a backup from 1 hours ago on site examplewebsite.com...1 hours Ago, the time was: 2021-10-10-14!We do have the 1 hours ago backup...Checking for a backup from 2 hours ago on site examplewebsite.com...2 hours Ago, the time was: 2021-10-10-13!We do have the 2 hours ago backup...Checking for a backup from 3 hours ago on site examplewebsite.com...3 hours Ago, the time was: 2021-10-10-12!We do have the 3 hours ago backup...Checking for a backup from 4 hours ago on site examplewebsite.com...4 hours Ago, the time was: 2021-10-10-11!We do have the 4 hours ago backup...Checking for a backup from 5 hours ago on site examplewebsite.com...5 hours Ago, the time was: 2021-10-10-10!We do have the 5 hours ago backup...Checking for a backup from 6 hours ago on site examplewebsite.com...6 hours Ago, the time was: 2021-10-10-09!We do have the 6 hours ago backup...Checking for a backup from 7 hours ago on site examplewebsite.com...7 hours Ago, the time was: 2021-10-10-08!We do have the 7 hours ago backup...Checking for a backup from 8 hours ago on site examplewebsite.com...8 hours Ago, the time was: 2021-10-10-07!We do have the 8 hours ago backup...Checking for a backup from 9 hours ago on site examplewebsite.com...9 hours Ago, the time was: 2021-10-10-06!We do have the 9 hours ago backup...Checking for a backup from 10 hours ago on site examplewebsite.com...10 hours Ago, the time was: 2021-10-10-05!We do have the 10 hours ago backup...Checking for a backup from 11 hours ago on site examplewebsite.com...11 hours Ago, the time was: 2021-10-10-04!We do have the 11 hours ago backup...Checking for a backup from 12 hours ago on site examplewebsite.com...12 hours Ago, the time was: 2021-10-10-03!We do have the 12 hours ago backup...Recording all available backups for the last 12 hours on site examplewebsite.com...Backups ENVironment file for site examplewebsite.com exists...Checking for a backup from 1 days ago on site examplewebsite.com...1 days Ago, the time was: 2021-10-09!We do have the 1 days ago backup...Checking for a backup from 2 days ago on site examplewebsite.com...2 days Ago, the time was: 2021-10-08!We do have the 2 days ago backup...Checking for a backup from 3 days ago on site examplewebsite.com...3 days Ago, the time was: 2021-10-07!We do have the 3 days ago backup...Checking for a backup from 4 days ago on site examplewebsite.com...4 days Ago, the time was: 2021-10-06!We do have the 4 days ago backup...Checking for a backup from 5 days ago on site examplewebsite.com...5 days Ago, the time was: 2021-10-05!We do have the 5 days ago backup...Checking for a backup from 6 days ago on site examplewebsite.com...6 days Ago, the time was: 2021-10-04!We do have the 6 days ago backup...Checking for a backup from 7 days ago on site examplewebsite.com...7 days Ago, the time was: 2021-10-03!We do have the 7 days ago backup...Recording all available backups for the last 7 days on site examplewebsite.com...Backups ENVironment file for site examplewebsite.com exists...Checking for a backup from 1 weeks ago on site examplewebsite.com...Checking interval 8 to 14 daysWe do have the 1 weeks ago backup...2021-09-30Checking for a backup from 2 weeks ago on site examplewebsite.com...Checking interval 15 to 21 daysWe do have the 2 weeks ago backup...2021-09-19Checking for a backup from 3 weeks ago on site examplewebsite.com...Checking interval 22 to 28 daysWe do have the 3 weeks ago backup...2021-09-12Checking for a backup from 4 weeks ago on site examplewebsite.com...Checking interval 29 to 35 daysWe do have the 4 weeks ago backup...2021-09-05Recording all available backups for the last 4 weeks on site examplewebsite.com...Backups ENVironment file for site examplewebsite.com exists...Checking for a backup from 1 months ago on site examplewebsite.com...Checking interval 36 to 56 daysWe do have the 1 months ago backup...2021-08-31Checking for a backup from 2 months ago on site examplewebsite.com...Checking interval 56 to 84 daysWe do have the 2 months ago backup...2021-07-31Checking for a backup from 3 months ago on site examplewebsite.com...Checking interval 84 to 112 daysRecording all available backups for the last 3 months on site examplewebsite.com...Backups ENVironment file for site examplewebsite.com exists...Recording all available backups for the last 3 MANUAL on site examplewebsite.com...Backups ENVironment file for site examplewebsite.com exists...Parsing the available backups from examplewebsite.com in the backups.env file...Sending available backups back to HQ...% Total % Received % Xferd Average Speed Time Time Time CurrentDload Upload Total Spent Left Speed100 180 0 0 100 180 0 412 --:--:-- --:--:-- --:--:-- 412
```

With this information, we can use the timestamp to restore a website like this:

```
gprestore site.url rollback {timestamp}
```

For example:

```
gprestore examplewebsite.com rollback 2021-09-19
```

#### Additional Acceptable Format:

For the previous 12 hours you can also use the following format:

```
gprestore site.url rollback {1-12)
```

“1” being the most recent.

For example, the following will roll the website back to the 3rd most recent backup:

```
gprestore examplewebsite.com rollback 3
```

 

## Prune Backups

First, display the passphrase for Borg with the following command:

```
cat /root/gridenv/backups.token
```

Then use any of the following commands, adjusting the retention levels as needed:

```
borg prune -v --keep-hourly=1 /opt/gridpane/backups/snapshotsborg prune -v --keep-daily=1 /opt/gridpane/backups/snapshotsborg prune -v --keep-weekly=1 /opt/gridpane/backups/snapshotsborg prune -v --keep-monthly=1 /opt/gridpane/backups/snapshots
```

### My Token Doesn’t Work

If for some reason the token doesn’t work, try this instead:

```
cat /root/gridpane.token
```

 

## Backups Aren’t Running Troubleshooting Steps

### 1. Check the Schedule

Check the cronjob exists with:

```
crontab -l
```

You should see this line:

```
0 * * * * /usr/local/bin/gpbup
```

If the gpbup cronjob is showing in crontab and backups are still not running, there are two things you can check.

### 2. Check for broken lock

Run a backup from the command line with bash -x in front of it to see the output.

For example:

```
bash -x gpbup site.url
```

Look for a system lock error. It may advise that you’re out of allocated space, or might just be locked. If space is an issue, you need to prune backups and/or increase allocated space. Repair and Rebuild once you’re done.

If it’s locked, you can break the lock with:

```
borg break-lock /opt/gridpane/backups/snapshots
```

### 3. Check the schedule

Look in this file:

```
cat /var/www/site.url/logs/backups.env
```

Unless it’s been changed, it should look something like this (depending on how long your backups have been running):

```
Local-Backups:ONRemote-Backups:ONHOURLY:1,2,3,4,5,6,7,8,9,10,11,12DAILY:1,2,3,4,5,6,7WEEKLY:2,3,4MONTHLY:1,2,3MANUAL:
```

That is saying to keep 12 hourly backups, 7 daily backups, and 3 weekly backups. If it doesn’t have that, edit the file and add those in. All env files are immutable, so you’ll need to use chattr on them in order to edit.

```
chattr -i backups.env
```

```
nano backups.env
```

```
chattr +i backups.env
```

### gpbup – Operation not permitted

If you’re finding that backups are not permitted run:

```
cd /var/www/site.url/logs
```

```
chattr -i backup.env
```

And try running the command again.

Example error:

```
Backups ENVironment file for site website.com exists...
sed: cannot rename /var/www/website.com/logs/sedvgPgPl: Operation not permitted
/usr/local/bin/gpbup: line 2070: /var/www/website.com/logs/backups.env: Operation not permitted
```

 

## Borg Repair and Rebuild

The following is how to run a repair

### Step 1. Display the Borg Passphrase

First, display the passphrase for Borg with the following command:

```
cat /root/gridpane.token
```

OR, if that doesn’t work:

```
cat /root/gridenv/backups.token
```

### Step 2. Run the Check and Repair

Next we’ll initiate Borg’s built in check and repair function with this command:

```
borg check --repair /opt/gridpane/backups/snapshots
```

Another way is to run the command with optional -v and -p which will show verbose output and each step as it progresses.

```
borg -p -v check --repair /opt/gridpane/backups/snapshots
```

When prompted, type YES.

After typing YES, it may just sit there for a moment. Be patient. At some point, it will ask for a passphrase. Use the one displayed in the first step.

Paste in the passphrase and hit Enter.

Be aware that the cursor will just sit there once you paste it in but the rebuild has started. It may take a minute, it may take an hour. That all depends on long the server has been running. All the while, it will sit there looking like its not doing anything, but rest assured it is.

When it’s done, it’ll just go back to the prompt. No confirmation, no celebration, just done. The below image shows this process in its entirety.

Full documentation of Borg can be found here:

https://borgbackup.readthedocs.io/en/stable/installation.html

 

## Downloading Local Backups

Backup of the current site can be downloaded from the site customizer using theSFTP download export option. To select other backup options, you need to access the server via SSH as `root` then use borg commands to extract the archive. Here are the steps to take. First, you will need to grab the borg password by running this command:```
cat /root/gridenv/backups.token
```

Then you will need to list the backups available on the server.

```
borg list /opt/gridpane/backups/snapshots
```

Or you can list backups for a specific site using this command:

```
/usr/bin/borg list /opt/gridpane/backups/snapshots --prefix $site
```

then here is the command to extract:

```
borg export-tar /opt/gridpane/backups/snapshots::{name.of.snapshot} /path/to/output/name.tar.gz
```

Ex.:

```
borg export-tar /opt/gridpane/backups/snapshots::example.com-2021-06-20-23 /var/www/example.com/example.com-SFTP-export.tar.gz
```

Replace example.com with your site domain.

 

## Modifying the Local Backup Schedule

Local backups for all of your websites are managed as a cronjob. If you’d like to change the frequency of your backup schedule, the information below will get you going. This is particularly useful for those of you who run large websites that take a significant amount of time to backup – WaaS sites are a popular one that struggle with hourly backups

There is a cronjob for a process called gpbup in your crontab. You can see your crontab by running this command:

```
crontab -l
```

The line you are looking for looks like this:

```
0 * * * * /usr/local/bin/gpbup
```

The zero and the stars correspond to times. What the above is saying is to run the command gpbup(GridPane Backup) located in /usr/local/bin at minute zero of every hour, of every day, of every month, of every week. This is what is setup on your servers by default.

To change the schedule, you can adjust those values. Luckily for us, some awesome soul created https://crontab.guru that will help you set your own custom schedule, and below are some examples to get you started.

Example 1

Let’s say you want to change your backup schedule to twice a day. It’s best to keep it on the hour – the script likes that. Here is what we would use to change it to at the zero minutes of hours 0 and 12 (that’s 0 and 12 UTC by default, adjust for your timezone). That line would look like this:

```
0 0,12 * * * /usr/local/bin/gpbup
```

Example 2

If you wanted to change the frequency to once every 4 hours you could do:

```
0 0,4,8,12,16,20 * * * /usr/local/bin/gpbup
```

This schedule would run backups at 12am, 4am, 8am, 12pm, 4pm and 8pm. The image below highlights the hourly part of the schedule.

Example 3

If you wanted to change the frequency to once every 8 hours you could do:

```
0 0,8,16 * * * /usr/local/bin/gpbup
```

This schedule would run backups at 12am, 8am, and 4pm.

### Editing the crontab

The command crontab -l only views the crontab. To edit the crontab you can run:

```
crontab -e
```

If you are presented with a choice, select nano as your editing tool. Then simply change the values on that line to set your schedule. Control+O will save the file (then press enter) and Control+X will close the file.

You can view the crontab again with crontab -l to confirm the changes, and you’re now all set.

### Cronjobs and Timezone

By default your servers will be on UTC time. You can confirm this by running:

```
date
```

If you’d like to set your cronjobs to run specific to your timezone, you can change your timezone (GP CLI coming soon).

First run the following to list available timezones:

```
timedatectl list-timezones
```

Use your down-arrow key to navigate down until you find your timezone, and hit Control+C to exit once you’ve got it.

You can now reset your timezone with this command:

```
sudo timedatectl set-timezone
```

Examples:

```
sudo timedatectl set-timezone Europe/Paris
```

```
sudo timedatectl set-timezone Asia/Singapore
```

```
sudo timedatectl set-timezone America/New_York
```

 

## Further Reading

For further information about how backup systems work, the available options for configuring them, and for setting up remote backups (available on V2), please see the articles listed below.

### Strategy

Recommended Backup Strategy

### V2 Backup Documentation

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

