# Transitioning from V1 (Legacy) Backups to V2 Backups | GridPane

# Transitioning from V1 (Legacy) Backups to V2 Backups

 

6 min read 

### Table of Contents

 

## Introduction

With the impending EOL of Borg, the V1 Backups system on December 17th 2021, this article contains multiple ways to update your servers and remove some of the pain of moving away from backups V1 to the new V2 system.

Before doing anything, we strongly recommend that you take a snapshot of your server at your provider. This way your original Borg backups will remain around no matter what happens in the future, and you can restore a server at the provider and run the Borg commands to grab the backups.

### Borg Commands

A list of Borg commands for any users who choose to continue to use backups V1 and Borg beyond the EOL date can be found in the following article:

GridPane V1 Local Backups

 

## Updating a server and sites directly by SSH and GP-CLI

Below details the available gp-cli commands for manual use.

Before running these commands, please run the following to make sure you have the latest scripts first:

```
gpupdate
```

 

### Update Server Backup System to V2

If you want to just enable the new backups system but not enable local backups for your sites on that server you can run:

```
gpbup -update-gridpane-backups-system
```

However, if you want to both update the server to backups v2 and enable automated local backups for all sites on your server then this is the command:

```
gpbup -update-gridpane-backups-system -enable-local-on-all-sites
```

 

### Enable/Disable Remote Automated Backups

These are obviously only useful once you have added a remote storage option to any site. It is not possible to add a remote storage provider by CLI, this action must be carried out from the UI or API.

But once a remote provider has been added, then these two matching remote CLI commands become useful. Here is how to enable/disable automated remote backups for a specific site on a server:

```
gpbup {your.site} -remote-bup-on
gpbup {your.site} -remote-bup-off
```

Here is how to enable/disable automated remote backups for all sites on a server:

```
gpbup all-sites -remote-bup-on
gpbup all-sites -remote-bup-off
```

NOTE: For remote backups, the provider will need to be manually added to the website within the UI or via API first (this has to take place via the App), before running the GP-CLI command to turn them on.

 

### Set Local/Remote Backups Schedule

Set a backup schedule for a single site:

```
gpbup {your.site} -set-backup-schedule \
-storage {string} \
-backup-interval {interval} \
-minute {integer} \
-hour {integer} \
-day {day}
```

Set a backup schedule for all sites on a server:

```
gpbup all-sites -set-backup-schedule \
-storage {string} \
-backup-interval {interval} \
-minute {integer} \
-hour {integer} \
-day {integer}
```

-storage accepts local || aws-s3 || backblaze || dropbox || wasabi

-backup-interval accepts hourly || daily || weekly || monthly

-minute accepts 0-59

-hour accepts 0-23

-day if -backup-interval weekly accepts 0-6 (0 == Sunday)

-day if -backup-interval monthly accepts 1-28

#### Example

Here’s an example of setting all sites on a server to backup on the 15th day of the month at 2.30 AM:

```
gpbup all-sites -set-backup-schedule -storage local -backup-interval monthly -minute 30 -hour 2 -day 15
```

 

### Set Local/Remote Prune Schedules

Set the pruning schedule for a single site:

```
gpbup {your.site} -set-prune-schedule {storage_type} {schedule_id} {retain_days}
```

Set the pruning schedule for all sites on a server:

```
gpbup all-sites -set-prune-schedule {storage_type} {schedule_id} {retain_days}
```

storage_type (string) accepts local || remote

schedule_id (integer) accepts the following range:

retain_days accepts the following range:

#### Example

Here’s an example of setting the local pruning schedule for all sites on a server to keep daily backups for 180 days:

```
gpbup all-sites -set-prune-schedule local 0 180
```

 

### Set server daily backup prune time

```
gpbup -set-prune-time {HH:MM}
```

-set-prune-time accepts HH:MM

This needs to be set in 24-hour format without seconds. For example, here’s how to set the pruning time to 2 AM:

```
gpbup -set-prune-time 02:00
```

 

## Updating a server and all sites directly via the application

If you are not comfortable with SSH, then you have the option to enable automated local backups for all sites on a server when you update that server to backups v2.

Click the checkbox when you enable the system, and that is it. It will set a schedule to midnight.

 

## Updating a server and all sites via the API

 

 

### Information

This is only available to Dev/Agency users with API access.

### Checking Which Servers Need Updating

You can use the following endpoints to find out if your servers are on version 1 or 2 of our backups system:

```
GET /server
GET /server/{server.id}
```

Links to Docs:GET single serverGET all servers

In the JSON object for each server you will see this if the server is on backups v2:

```
{
   ....
"update_backups": true
   ....
}
```

Or this if the server is still on backups v1:

```
{
   ....
"update_backups": false
   ....
}
```

You can then use the PUT to update the server to v2 if needed, and optionally enable local remote backups for all sites on the server at the same time.

```
PUT
/server/{server.id}
```

```
{"update_backups_system": true
"enable_site_local_backups": true || false
}
```

Link to Docs:PUT update server backups

If you want to update your sites on a site by site basis, with different settings, then you can do this by the API:POST Add a remote backup integration to a sitePUT enable/disable automated backupsPUT Update the site backup schedules

 

### Bash Script

This is a little script we’ve been using in testing. To use this, just need to swap in your Oauth Key (and the GridPane URL if you’re on your own Agency instance), and set whether you want backups to be enabled. Make sure the script file is executable and then run it.

It will loop through about 2 servers a minute to handle the rate limits and resources, but it is pretty much run it and forget it:

 

```
#!/bin/bash

# Enter your OAuth API key below
API_KEY="XXXXX"

# If on Agency please update to your instance domain
gp_url="my.gridpane.com"

# Set to false if you do not want to enable local backups for all the sites on your server
enable_local_backups="true"

update_backups_system() {
  for ((i = 1; i <= 100; i++)); do
    local servers
    servers=$(curl --location --request GET "https://${gp_url}/oauth/api/v1/server?page=$i&per_page=200" --header 'Authorization: Bearer '${API_KEY}'')
    while [[ ${servers} == *"Beep, Beep"* ]]; do
      echo "Sleeping for rate limit.... 31 seconds"
      sleep 31
      servers=$(curl --location --request GET "https://${gp_url}/oauth/api/v1/server?page=$i&per_page=200" --header 'Authorization: Bearer '${API_KEY}'')
    done

    local servers_per_page
    servers_per_page=$(echo ${servers} | jq '.data' | jq length)
    if [[ "${servers_per_page}" -eq 0 ]]; then
      printf "\n--------------------------------------------------\n"
      echo "And we are done.... exiting..."
      echo
      break
    fi

    local servers_per_page_zero_indexed
    servers_per_page_zero_indexed=$((servers_per_page - 1))
    for ((x = 0; x <= servers_per_page_zero_indexed; x++)); do
      local server_id
      server_id="$(echo ${servers} | jq '.data['$x'].id')"
      printf "\n--------------------------------------------------\n"
      echo "Server ID: ${server_id}"
      echo "Server host: $(echo ${servers} | jq '.data['$x'].label')"
      echo "IP: $(echo ${servers} | jq '.data['$x'].ip')"
      local updated_state
      updated_state="$(echo ${servers} | jq '.data['$x'].update_backups')"
      echo "Backups Updated: ${updated_state}"
      if [[ ${updated_state} == *"true"* ]]; then
        echo "--------------------------------------------------"
        continue
      fi

      echo "updating to new system..."
      [[ ${enable_local_backups} == "true" ]] &&
        echo "and enabling local backups for all sites..."

      local update_backup_system
      update_backup_system=$(
        curl --location --request PUT "https://${gp_url}/oauth/api/v1/server/${server_id}" \
          --header 'Authorization: Bearer '${API_KEY}'' \
          --header 'Content-Type: application/json' \
          --data-raw '{ "update_backups_system": true, "enable_site_local_backups": '${enable_local_backups}' }'
      )
      while [[ ${update_backup_system} == *"Beep, Beep"* ]]; do
        echo "Sleeping for rate limit.... 31 seconds"
        sleep 31
        update_backup_system=$(
          curl --location --request PUT "https://${gp_url}/oauth/api/v1/server/${server_id}" \
            --header 'Authorization: Bearer '${API_KEY}'' \
            --header 'Content-Type: application/json' \
            --data-raw '{ "update_backups_system": true, "enable_site_local_backups": '${enable_local_backups}' }'
        )
      done
      echo "${update_backup_system}"
      echo "--------------------------------------------------"
      echo "Sleeping for rate limit.... 31 seconds"
      sleep 31
    done
  done
}
update_backups_system
```

### Additional Note: Customising the Above Script for Remote Backups

For those of you who are proficient in Bash and would like to mass enable remote backups across your websites, you could look at modifying the above script using the following to identify the integration IDs for your remote backup provider of choice:

```
GET /integration
```

You could then loop through all of your sites (or all sites on a particular server) using:

```
GET /siteGET /server
```

If you wanted to only add remote backups to certain sites, you could potentially create a variable with delimiters, for example:

```
:site.com:other.site:next.site
```

And have the loop check for those:

```
!= *":${site}:"* ]]; thencontinue
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

