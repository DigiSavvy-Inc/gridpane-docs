# GP-CLI Quick Reference | GridPane

# GP-CLI Quick Reference

 

12 min read 

### Table of Contents

 

## Quick Intro

 

This article details all of the available GP CLI commands that you can run on your GridPane servers. It’s rapid-fire, and so doesn’t go into any in-depth explanations, but the detailed Knowledge Base articles that go into detail are linked beneath the title of each section. We strongly recommend that you refer to the dedicated articles to ensure correct usage.

We’ll keep this article up-to-date as more GP CLI commands are released/updated in the future.

 

## Nginx

### Nginx Services

Full article: Service Management: Nginx

```
gp ngx -t
```

```
gp ngx -status
```

```
gp ngx -stopgp ngx -start
```

```
gp ngx -reloadgp ngx -restart
```

### Nginx Stack

The GP-CLI commands below are thoroughly detailed in our Configure Nginx article. If you’re unsure about how or if you should use any of these commands, please read this before running any of them on your servers. They’re included here only for reference purposes.

Full article: Configure Nginx

GeoIP2

```
gp stack nginx geoip -on {account.id}:{license.key}
gp stack nginx geoip -off
```

```
gp stack nginx geoip -update {iso.code}:{yes.no},{iso.code}:{yes.no}gp stack nginx geoip -remove {iso.code},{iso.code},{iso.code}
```

Configure Nginx Workers

```
gp stack nginx worker -connections {integer}
```

```
gp stack nginx worker -rlimit-nofile {integer}
```

Server Name Configurations

```
gp stack nginx server-name -in-redirect {accepted.value}
```

```
gp stack nginx server-name -hash-bucket-size {accepted.integer}
```

Limit Configurations

```
gp stack nginx limits -client-body-buffer-size {accepted.integer}
```

```
gp stack nginx limits -client-body-timeout {accepted.integer}
```

```
gp stack nginx limits -client-header-buffer-size {accepted.integer}
```

```
gp stack nginx limits -client-header-timeout {accepted.integer}
```

```
gp stack nginx limits -keepalive-requests {accepted.integer}
```

```
gp stack nginx limits -keepalive-timeout {accepted.integer}
```

```
gp stack nginx limits -large-client-headers-buffers {b.quantity} {b.size}
```

```
gp stack nginx limits -req-zone-one {store.size.mb} {req.per.sec}
```

```
gp stack nginx limits -req-zone-wp {store.size.mb} {req.per.sec}
```

```
gp stack nginx limits -reset-timedout-connection {accepted.value}
```

```
gp stack nginx limits -send-timeout {accepted.value}
```

```
gp stack nginx limits -types-hash-max-size {accepted.value}
```

Open File Cache Configurations

```
gp stack nginx open-file-cache -max {elements} -inactive {timeout}
```

```
gp stack nginx open-file-cache -errors {accepted.value}
```

```
gp stack nginx open-file-cache -min-uses {accepted.value}
```

```
gp stack nginx open-file-cache -valid {accepted.value}
```

FastCGI Configurations

```
gp stack nginx fastcgi -buffering {accepted.value}
```

```
gp stack nginx fastcgi -buffers {b.quantity} {b.size}
```

```
gp stack nginx fastcgi -buffer-size {accepted.value}
```

```
gp stack nginx fastcgi -busy-buffers-size {accepted.value}
```

```
gp stack nginx fastcgi -cache-background-update ongp stack nginx fastcgi -cache-background-update off
```

```
gp stack nginx fastcgi -max-cache-size {accepted.value}
```

```
gp stack nginx fastcgi -cache-revalidate {accepted.value}
```

```
gp stack nginx fastcgi -connect-timeout {accepted.value}
```

```
gp stack nginx fastcgi -keep-connections {accepted.value}
```

```
gp stack nginx fastcgi -read-timeout {accepted.value}
```

```
gp stack nginx fastcgi -send-timeout {accepted.value}
```

Proxy Configurations

```
gp stack nginx proxy -buffering ongp stack nginx proxy -buffering off
```

```
gp stack nginx proxy -buffers {b.quantity} {b.size}
```

```
gp stack nginx proxy -buffer-size {accepted.value}
```

```
gp stack nginx proxy -busy-buffers-size {accepted.value}
```

```
gp stack nginx proxy -cache-background-update ongp stack nginx proxy -cache-background-update off
```

```
gp stack nginx proxy -max-cache-size {accepted.value}
```

```
gp stack nginx proxy -cache-revalidate ongp stack nginx proxy -cache-revalidate off
```

```
gp stack nginx proxy -connect-timeout {accepted.value}
```

```
gp stack nginx proxy -keep-connections ongp stack nginx proxy -keep-connections off
```

```
gp stack nginx proxy -read-timeout {accepted.value}
```

```
gp stack nginx proxy -send-timeout {accepted.value}
```

Limits Configurations

```
gp stack nginx limits -site-zone-one-burst {queue.size} {site.url}
```

```
gp stack nginx limits -site-zone-wp-burst {queue.size} {site.url}
```

FastCGI Configurations

```
gp stack nginx limits -site-max-body-size {accepted.value} {site.url}
```

```
gp stack nginx fastcgi -site-cache-valid {accepted.value} {site.url}
```

Site Proxy Configurations

```
gp stack nginx proxy -site-cache-valid {accepted.value} {site.url}
```

```
gp stack nginx redis -site-cache-valid {accepted.value} {site.url}
```

### Nginx Hardening

Full article: Nginx Site Hardening with GP CLI

```
gp site {site.url} -disable-xmlrpc gp site {site.url} -enable-xmlrpc
```

```
gp site {site.url} -disable-concatenate-load-scriptsgp site {site.url} -enable-concatenate-load-scripts
```

```
gp site {site.url} -block-wp-content.phpgp site {site.url} -unblock-wp-content.php
```

```
gp site {site.url} -block-wp-comments-post.phpgp site {site.url} -unblock-wp-comments-post.php
```

```
gp site {site.url} -block-wp-links-opml.phpgp site {site.url} -unblock-wp-links-opml.php
```

```
gp site {site.url} -block-wp-trackbacks.phpgp site {site.url} -unblock-wp-trackbacks.php
```

```
gp site {site.url} -block-upgrade.phpgp site {site.url} -unblock-upgrade.php
```

```
gp site {site.url} -block-install.phpgp site {site.url} -unblock-install.php
```

 

back to top ▲

 

## PHP

### PHP Services

Full article: Service Management: PHP

```
gp php $version -stop gp php $version -start
```

```
gp php $version -reload gp php $version -restart
```

### PHP Stack

The GP-CLI commands below are thoroughly detailed in our Configure PHP article. If you’re unsure about how or if you should use any of these commands, please read this before running any of them on your servers. They’re included here only for reference purposes.

Full article: Configure PHP

Configure PHP by Version

```
gp stack php {php.version} -allow-url-fopen {accepted.value}
```

```
gp stack php {php.version} -allow-url-include {accepted.value}
```

```
gp stack php {php.version} -date-timezone {supported.timezone}
```

```
gp stack php {php.version} -default-socket-timeout {integer}
```

```
gp stack php {php.version} -max-exec-time {integer}
```

```
gp stack php {php.version} -max-file-uploads {integer}
```

```
gp stack php {php.version} -max-input-time {integer}
```

```
gp stack php {php.version} -max-input-vars {integer}
```

```
gp stack php {php.version} -post-max-size {integer}
```

```
gp stack php {php.version} -mem-limit {integer}
```

```
gp stack php {php.version} -session-cookie-lifetime {integer}
```

```
gp stack php {php.version} -session-gc-maxlifetime {integer}
```

```
gp stack php {php.version} -short-open-tag {on.off}
```

```
gp stack php {php.version} -upload-max-filesize {integer}
```

Configure PHP Opcache by Version

```
gp stack php {php.version} -opcache-enable
gp stack php {php.version} -opcache-disable
```

```
gp stack php {php.version} -opcache-enable-cli
gp stack php {php.version} -opcache-disable-cli
```

```
gp stack php {php.version} -opcache-max-accel-files {integer}
```

```
gp stack php {php.version} -opcache-memory {integer}
```

```
gp stack php {php.version} -opcache-reval-freq $int
```

Site PHP General Settings

```
gp stack php -site-date-timezone {supported.timezone} {site.url}
```

```
gp stack php -site-default-socket-timeout {integer} {site.url}
```

```
gp stack php -site-max-exec-time {integer} {site.url}
```

```
gp stack php -site-max-file-uploads {integer} {site.url}
```

```
gp stack php -site-max-input-time {integer} {site.url}
```

```
gp stack php -site-max-input-vars {site.ur;} {site.url}
```

```
gp stack php -site-mem-limit {integer} {site.url}
```

```
gp stack php -site-post-max-size {integer} {site.url}
```

```
gp stack php -site-session-cookie-lifetime {integer} {site.url}
```

```
gp stack php -site-session-gc-maxlifetime {integer} {site.url}
```

```
gp stack php -site-short-open-tag {on.off} {site.url}
```

```
gp stack php -site-upload-max-filesize {integer} {site.url}
```

Configure PHP Process Manager/Workers by Site

```
gp stack php -site-pm {accepted.value} {site.url}
```

```
gp stack php -site-pm-max-children {accepted.value} {site.url}
```

```
gp stack php -site-pm-max-requests {integer} {site.url}
```

```
gp stack php -site-pm-max-spare-servers {accepted.value} {site.url}
```

```
gp stack php -site-pm-min-spare-servers {accepted.value} {site.url}
```

```
gp stack php -site-pm-process-idle-timeout {integer} {site.url}
```

```
gp stack php -site-pm-start-servers {accepted.value} {site.url}
```

### Switch PHP Version

```
gp site {site.url} -switch-php $version
```

 

back to top ▲

 

## MySQL

### MySQL Services

Full article: Service Management: MySQL

```
gp mysql -stop 
gp mysql -start
```

```
gp mysql -reload
gp mysql -restart
```

### MySQL Stack

The GP-CLI commands below are thoroughly detailed in our Configure MySQL article. If you’re unsure about how or if you should use any of these commands, please read this before running any of them on your servers. They’re included here only for reference purposes.

Full article: Configure MySQL

```
gp stack mysql -binlog-expire-logs-seconds {accepted.value}
```

```
gp stack mysql -binlog-space-limit {accepted.value}
```

```
gp stack mysql -innodb-autoinc-lock-mode {accepted.value}
```

```
gp stack mysql -innodb-buffer-pool-instances {accepted.value}
```

```
gp stack mysql -innodb-buffer-pool-size {accepted.value}
```

```
gp stack mysql -innodb-flush-log-at-trx-commit {accepted.value}
```

```
gp stack mysql -innodb-flush-method {accepted.value}
```

```
gp stack mysql -innodb-io-capacity {accepted.value}
```

```
gp stack mysql -innodb-io-capacity-max {accepted.value}
```

```
gp stack mysql -innodb-log-file-size {accepted.value}
```

```
gp stack mysql -join-buffer-size {accepted.value}
```

```
gp stack mysql -long-query-time {accepted.value}
```

```
gp stack mysql -max-binlog-size {accepted.value}
```

```
gp stack mysql -max-connections {accepted.value}
```

```
gp stack mysql -slow-query-log {accepted.value}
```

```
gp stack mysql -long-query-time {accepted.value}
```

```
gp stack mysql -thread-handling {accepted.value}
```

```
gp stack mysql -thread-pool-high-prio-mode {accepted.value}
```

```
gp stack mysql -thread-pool-high-prio-tickets {accepted.value}
```

```
gp stack mysql -thread-pool-idle-timeout {accepted.value}
```

```
gp stack mysql -thread-pool-max-threads {accepted.value}
```

```
gp stack mysql -thread-pool-size {accepted.value}
```

```
gp stack mysql -thread-pool-stall-limit {accepted.value}
```

 

back to top ▲

 

## Redis

### Redis Services

Full article: Service Management: Redis

```
gp redis -stop gp redis -start
```

```
gp redis -reload gp redis -restart
```

### Redis Stack

The GP-CLI commands below are thoroughly detailed in our Configure Redis article. If you’re unsure about how or if you should use any of these commands, please read this before running any of them on your servers. They’re included here only for reference purposes.

Full article: Configure Redis

```
gp stack redis -evic-policy $key_eviction_policy $optional_max_memorygp stack redis -evic-policy-reset
```

```
gp stack redis -max-memory $integer_max_memorygp stack redis -max-memory-reset
```

```
gp stack redis -enable-persistencegp stack redis -disable-persistence
```

```
gp stack redis -reset
```

 

back to top ▲

 

## Domain Routing

NOTE: We recommend you use toggle inside your site settings.

Full article: Manage Site Domains and Site Routing (non www vs www)

```
gp site {site.url} -route-domain-www
gp site {site.url} -route-domain-root
gp site {site.url} -route-domain-off
```

 

back to top ▲

 

## Caching

Learn all about Server Caching here.NOTE: We recommend you use toggle inside your site settings.

The activation/deactivation commands below are for page caching. The number at the end indicates the default time-to-live (TTL) in seconds:

```
gp site {site.url} -redis-cache -ttl 2592000
gp site {site.url} -fastcgi-cache -ttl 1
gp site {site.url} -cache-off
```

You can activate/deactivate Redis Object caching for a specific site with:

```
gp site {site.url} -redis-object-caching on
gp site {site.url} -redis-object-caching off
```

You can clear ALL the caches for a specific site with:

```
gp fix cached {site.url}
```

If you would like to clear ALL caches for ALL websites on the server you can run:

```
gp fix cached
```

 

back to top ▲

 

## 6G WAF

Full article: Using the GridPane 6G WAF

```
gp site {site.url} -6g-ongp site {site.url} -6g-off
```

```
gp site {site.url} 6g -bad-bots ongp site {site.url} 6g -bad-bots off
```

```
gp site {site.url} 6g -bad-query-string ongp site {site.url} 6g -bad-query-string off
```

```
gp site {site.url} 6g -bad-referer ongp site {site.url} 6g -bad-referer off
```

```
gp site {site.url} 6g -bad-request on
gp site {site.url} 6g -bad-request off
```

```
gp site {site.url} 6g -bad-methods on
gp site {site.url} 6g -bad-methods off
```

 

## 7G WAF

Full article: Using the GridPane 7G WAF

```
gp site {site.url} -7g-ongp site {site.url} -7g-off
```

```
gp site {site.url} 7g -bad-bots ongp site {site.url} 7g -bad-bots off
```

```
gp site {site.url} 7g -bad-query-string ongp site {site.url} 7g -bad-query-string off
```

```
gp site {site.url} 7g -bad-referer ongp site {site.url} 7g -bad-referer off
```

```
gp site {site.url} 7g -bad-request on
gp site {site.url} 7g -bad-request off
```

```
gp site {site.url} 7g -bad-methods on
gp site {site.url} 7g -bad-methods off
```

 

back to top ▲

 

## Modsec WAF (ModSecurity)

Full article: Using the GridPane ModSec Web Application Firewall

```
gp site {site.url} -modsec-ongp site {site.url} -modsec-off
```

```
gp site {site.url} -modsec -paranoia-level {1-4}
```

```
gp site {site.url} -modsec -anomaly-threshold {integer}
```

 

back to top ▲

 

## Fail2Ban

Full article: Configuring Fail2Ban to Prevent Brute Force Attacks

```
gp site {site.url} -enable-wp-fail2ban gp site {site.url} -enable-wp-fail2ban -default-offgp site {site.url} -disable-wp-fail2ban
```

```
gp site {site.url} -configure-wp-fail2ban -block-user-enumerationgp site {site.url} -configure-wp-fail2ban -unblock-user-enumeration
```

```
gp site {site.url} -configure-wp-fail2ban -block-stupid-usernamesgp site {site.url} -configure-wp-fail2ban -unblock-stupid-usernames
```

```
gp site {site.url} -configure-wp-fail2ban -guard-commentsgp site {site.url} -configure-wp-fail2ban -unguard-comments
```

```
gp site {site.url} -configure-wp-fail2ban -guard-password-resetsgp site {site.url} -configure-wp-fail2ban -unguard-password-resets
```

```
gp site {site.url} -configure-wp-fail2ban -guard-pingbacksgp site {site.url} -configure-wp-fail2ban -unguard-pingbacks
```

```
gp site {site.url} -configure-wp-fail2ban -guard-spamgp site {site.url} -configure-wp-fail2ban -unguard-spam
```

```
gp site {site.url} -configure-wp-fail2ban -default
```

 

back to top ▲

 

## Backups

We recommend that you manage your backups directly in the UI wherever possible.

### Purge

```
gpbup {site.url} -purge {local/aws-s3/backblaze/wasabi/dropbox} "{date.string.from}" "{date.string.to}"
```

Example:

```
gpbup examplewebsite.com -purge local "2021-04-28 09:00" "2021-04-29 01:00"
```

### Update from V1 to V2

Learn more here: Transitioning from V1 Backups to V2 Backups

```
gpbup -update-gridpane-backups-system
```

Update and enable backups on all sites:

```
gpbup -update-gridpane-backups-system -enable-local-on-all-sites
```

### Enable/Disable Remote Automated Backus

```
gpbup {your.site} -remote-bup-on
gpbup {your.site} -remote-bup-off
```

```
gpbup all-sites -remote-bup-on
gpbup all-sites -remote-bup-off
```

### Set Local/Remote Backups Schedule

Set a backup schedule for a single site:

```
gpbup {your.site} -set-backup-schedule \-storage {string} \-backup-interval {interval} \-minute {integer} \-hour {integer} \-day {day}
```

Set a backup schedule for all sites on a server:

```
gpbup all-sites -set-backup-schedule \-storage {string} \-backup-interval {interval} \-minute {integer} \-hour {integer} \-day {integer}
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

### Set Server Daily Backup Prune Time

```
gpbup -set-prune-time {HH:MM}
```

 

back to top ▲

 

## WP Debug and Query Monitor

Full article: WordPress Debug and Query Monitor

```
gp site {site.url} -wp-debug-on
```

```
gp site {site.url} -wp-debug-off
```

 

back to top ▲

 

## GP-Cron

Full article: WP-Cron and GridPane’s GP-Cron

```
gp site {site.url} -gpcron-on {minute.interval}
```

```
gp site {site.url} -gpcron-off
```

 

back to top ▲

 

## Brotli

Full article: Brotli Compression and GridPane

```
gp site {site.url} -brotli-ongp site {site.url} -brotli-off
```

 

back to top ▲

 

## HTTP Auth

NOTE: We recommend you use toggle inside your site settings.

Full article: Activating HTTP Authentication on Your Website

```
gp site {site.url} -http-auth
gp site {site.url} -http-auth-off
```

 

back to top ▲

 

## Content Security Policy (CSP) Headers

Full article: How to create a Content Security Policy (CSP Header)

```
gp site {site.url} -csp-header-on gp site {site.url} -csp-header-off
```

 

back to top ▲

 

## Suspend/Disable a Site

Full article: Suspend/Disable a Site with GP-CLI

```
gp site {site.url} -suspendgp site {site.url} -unsuspend
```

```
gp site {site.url} -suspend -use-server-custom
```

```
gp site {site.url} -suspend -use-site-custom
```

 

back to top ▲

 

## GP WP-CLI

Full article: GridPane and WP-CLI

```
gp wp {site.url} {wp.cli.command} {arg} {arg} {arg} {arg.n}
```

 

back to top ▲

 

## Sync Settings

Sync settings across all sites with the GridPane dashboard.

```
gp site all-sites sync-php-settingsgp site all-sites sync-6g-settingsgp site all-sites sync-7g-settingsgp site all-sites sync-modsec-settingsgp site all-sites sync-wpf2b-settingsgp site all-sites sync-additional-security-settingsgp site all-sites sync-access-settingsgp site all-sites sync-nginx-cache-settingsgp site all-sites sync-object-cache-settings
```

 

## Fix Permissions

Tools article: Self Help Tools: Reset Application File Permissions

While resetting permissions is easily done inside of your account dashboard, you can also easily do this via GP-CLI directly on your server.

```
gp fix perms {site.url}
```

 

back to top ▲

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

