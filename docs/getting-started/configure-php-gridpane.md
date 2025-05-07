# Configure PHP | GridPane

# Configure PHP

 

31 min read 

 

### Update

Options for customizing PHP on your individual websites are now available directly inside the UI in your site customiser!

## Index

Configure PHP by Version

Configure PHP Opcache by Version

Configure PHP by Site

Configure PHP Process Manager/Workers by Site

How Your Site PHP Workers… work

▲

 

## Configure PHP by Version

These changes are recorded in each PHP versions php.ini which resides at the following filepath, replacing {php.version} with the version of PHP required:

```
/etc/php/{php.version}/fpm/php.ini
```

Settings configured in aphp.iniare global by nature and impact each WordPress site which uses that particular version of PHP, unless that site has a conflicting per site .user.ini setting, in which case the per-site configuration takes precedence.

In each command below, substitute your PHP version (7.2, 7.3, etc) in place of {php.version}.

Each command automatically reloads the requisite PHP version, however, if you are wishing to chain together several commands you may wish to use the -no-reload flag as the last argument. This will stop you from reloading PHP multiple times, after which you can reload php.

For example:

```
gp stack php 7.4 -mem-limit 512 -no-reload &&  
gp stack php 7.4 -max-exec-time 60 -no-reload && 
gp php 7.4 reload
```

back to top ▲

 

## PHP Version General Settings

These commands all take integer arguments, with the integer being converted into the required unit by the script. and impact all WordPress sites using that version of PHP.

▲

 

### Allow URL-aware fopen wrappers

Enable URL-aware fopen wrappers that enable accessing URL objects like files.

Directive: allow_url_fopenDefault value: onAccepted values: Boolean/on/off/On/Off/ON/OFF

```
gp stack php {php.version} -allow-url-fopen {accepted.value}
```

Example:

```
gp stack php 7.4 -allow-url-fopen on
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

 

### Allow URL-aware fopen wrappers with include functions

NOTE: This requires allow_url_fopen=On or will not work.

Allows the use of URL-aware fopen wrappers with the following functions:

include, include_once, require, require_once

 

 

### Deprecation Notice

As of PHP 7.4, this function has been deprecated.

Directive: allow_url_includeDefault value: offAccepted values: Boolean/on/off/On/Off/ON/OFFRequires: allow_url_fopen = on

```
gp stack php {php.version} -allow-url-include {accepted.value}
```

Example:

```
gp stack php 7.4 -allow-url-include on
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

▲

 

### Set The default timezone used by all date/time functions

Sets The default timezone used by all date/time functions. The precedence order for which timezone is used if none is explicitly mentioned is described in the date_default_timezone_get() page at php.net. Please check this list of supported timezones at php.net.

Directive: date.timezoneDefault value: NULLAccepted Values: {supported.timezone} (String)

```
gp stack php {php.version} -date-timezone {supported.timezone}
```

Example:

```
gp stack php 7.4 -date-timezone Pacific/Honolulu
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the socket/stream wait timeout for a PHP script

The socket/stream wait time is not included in PHPs max execution time. The default socket timeout in PHP is 60 seconds. HTTP requests performed with some functions may exceed the execution time due to this wait being too short. Examples of such functions include:

file_get_contents, fopen or curl

Directive: default_socket_timeoutUnit: SecondsDefault value: 60

```
gp stack php {php.version} -default-socket-timeout {integer}
```

Example:

```
gp stack php 7.4 -default-socket-timeout 300
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the maximum execution time for each PHP script

Set the maximum time in seconds a script is allowed to run before it is terminated by the parser.

Directive: max_execution_timeUnit: SecondsDefault value: 300

```
gp stack php {php.version} -max-exec-time {integer}
```

Example:

```
gp stack php 7.4 -max-exec-time 300
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the maximum number of files that can be upload via a single request by a PHP script

The maximum number of files allowed to be uploaded simultaneously. Upload fields left blank on submission do not count towards this limit.

Directive: max_files_uploadUnit: FilesDefault value: 20

```
gp stack php {php.version} -max-file-uploads {integer}
```

Example:

```
gp stack php 7.4 -max-file-uploads 1024
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the maximum input time for each PHP script

Set the maximum time in seconds a script is allowed to parse input data, like POST and GET. Timing begins at the moment PHP is invoked at the server and ends when execution begins. Set to 0 to allow unlimited time.

Directive: max_input_timeUnit: SecondsDefault value: 60

```
gp stack php {php.version} -max-input-time {integer}
```

Example:

```
gp stack php 7.4 -max-input-time 120
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set how many GET/POST/COOKIE input variables may be accepted by a PHP script.

How many input variables may be accepted (limit is applied to $_GET, $_POST and $_COOKIE superglobal separately). Use of this directive mitigates the possibility of denial of service attacks that use hash collisions.

Directive: max_input_varsUnit: VariablesDefault value: 5000

```
gp stack php {php.version} -max-input-vars {integer}
```

Example:

```
gp stack php 7.4 -max-input-vars 10000
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the memory limit for each PHP script

Set the maximum amount of memory that a script is allowed to allocate. This helps prevent poorly written scripts for eating up all available memory on a server. Note that to have no memory limit, set this directive to -1.

Directive: memory_limitUnit: MBDefault value: 256

```
gp stack php {php.version} -mem-limit {integer}
```

Example:

```
gp stack php 7.4 -mem-limit 512
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the maximum post size per PHP script

Sets max size of post data allowed.  To upload large files, this value must be larger than upload_max_filesize.  Generally speaking, this should also be smaller than the set memory_limit.

Directive: post_max_sizeUnit: MBDefault value: 512

```
gp stack php {php.version} -post-max-size {integer}
```

Example:

```
gp stack php 7.4 -post-max-size 1024
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the session cookie lifetime for a cookie created by a PHP script

Specify the lifetime of a cookie in seconds which is sent to the browser. The value 0 means “until the browser is closed.”

Directive: session.cookie_lifetimeUnit: SecondsDefault value: 0

```
gp stack php {php.version} -session-cookie-lifetime {integer}
```

Example:

```
gp stack php 7.4 -session-cookie-lifetime 3600
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the garbage collection for data created by a PHP script

Specify the number of seconds after which data will be seen as ‘garbage’ and potentially cleaned up.

Directive: session.gc_maxlifetimeUnit: SecondsDefault value: 1440

```
gp stack php {php.version} -session-gc-maxlifetime {integer}
```

Example:

```
gp stack php 7.4 -session-gc-maxlifetime 3600
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Enable the short form of PHP’s open tag

Tells PHP whether the short form <? ?> of PHP’s open tag should be allowed. Disabled by default, so it is possible to use PHP in combination with XML inline <? xml ?>. If you enable this option and have difficulties with xml inline, please remember to echo the XML'; ?>.

Directive: short_open_tagAccepted values: on | offDefault value: off

```
gp stack php {php.version} -short-open-tag {on.off}
```

Example:

```
gp stack php 7.4 -short-open-tag on
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

### Set the maximum upload file size each PHP script allows

Set the maximum size allowed for an uploaded file by a PHP script.

Directive: upload_max_filesizeUnit: MBDefault value: 512

```
gp stack php {php.version} -upload-max-filesize {integer}
```

Example:

```
gp stack php 7.4 -upload-max-filesize 1024
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

back to top ▲

 

## Configure PHP Version OPcache Settings

OPcache provides an improvement to PHP performance by storing precompiled script bytecode in shared memory, thereby removing the need for PHP to load and parse scripts on each request.

back to top ▲

▲

### Enable/Disable OPcache

Directive: opcache.enableDefault value: enabled

```
gp stack php {php.version} -opcache-enable
gp stack php {php.version} -opcache-disable
```

Example:

```
gp stack php 7.4 -opcache-enable
```

Optional last flag: -no-reload

This directive can only be set by gp-cli at the PHP version level.

back to top ▲

▲

### Enable/Disable CLI

Directive: opcache.enable_cliDefault value: disabled(primarily used for debugging issues with OPcache itself, not suitable for most users)

```
gp stack php {php.version} -opcache-enable-cli
gp stack php {php.version} -opcache-disable-cli
```

Example:

```
gp stack php 7.4 -opcache-enable-cli
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

▲

### Set the number of Opcache Accelerated Files

This is the maximum number of keys (and therefore scripts) in the OPcache hash table. The larger the number, the more scripts that will be hashed. Although you set the value, the actual value which will be used is the first number in the set of prime numbers { 223, 463, 983, 1979, 3907, 7963, 16229, 32531, 65407, 130987 } that is greater than or equal to the configured value. The minimum value is 200, default is 10000, and maximum is 1000000 in PHP 7.x.

Directive: opcache.max_accelerated_filesUnit: MBDefault value: 10000

```
gp stack php {php.version} -opcache-max-accel-files {integer}
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

▲

### Set an Opcache Memory Limit

Change the size of the shared memory storage used by OPcache, in megabytes.

Directive: opcache.memory_consumptionUnit: MBDefault value: 64

```
gp stack php {php.version} -opcache-memory {integer}
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

▲

### Set the Opcache Revalidation Frequency

This value determines who often to check script timestamps for updates and it expressed in seconds. A value of 0 will result in OPcache checking for updates with every request. The default value is 60.

Directive: opcache.revalidate_freqUnit: SecondsDefault value: 60

```
gp stack php {php.version} -opcache-reval-freq $int
```

Optional last flag: -no-reload

This directive can only be set at the PHP version level.

back to top ▲

 

## Configure PHP by site

 

We highly recommend you use the new tab inside your GridPane account dashboard to make any PHP changes you need, but the GP CLI detailed below is all still correct for everyone who prefers working via CLI.

You can open up your site customizer by clicking the domain name of site inside the Sites page of your GridPane account.

PHP settings are inside the PHP tab. Before you can make changes you may need to sync your settings. You can do this by clicking the Sync PHP Settings button:

 

These settings only impact the site for which they are set. The changes are written to a .user.ini which resides at the following filepath:

```
/var/www/{site.url}/htdocs/.user.ini
```

(by SSH/SFTP as root)

```
/Sites/{site.url}/htdocs/.user.ini
```

(by SSH/SFTP as system user)

In each command below, substitute your site for {site.url}.

Each command automatically reloads the requisite PHP version for that site, however if you are wishing to chain together several commands you may wish to use the -no-reload flag as the last argument. This will stop you from reloading PHP multiple times, after which you can reload php.

For example:

```
gp stack php -site-mem-limit 512 gridpane.com -no-reload &&  
gp stack php -site-max-exec-time 60 gridpane.com -no-reload && 
gp php 7.4 reload
```

back to top ▲

 

## Site PHP General Settings

These commands all take integer arguments, with the integer being converted into the required unit by the script. and impact all WordPress sites using that version of PHP.

You may notice many of these commands will configure the parameters identical to those at the PHP version level. As noted below each script that is affected, configuring these parameters at a site level will take precedence over the values set at the PHP version level.

▲

### Set The default timezone used by all date/time functions.

Sets The default timezone used by all date/time functions. The precedence order for which timezone is used if none is explicitly mentioned is described in the date_default_timezone_get() page at php.net. Please check this list of supported timezones at php.net.

Directive: date.timezoneDefault value: NULLAccepted Values: {supported.timezone} (String)

```
gp stack php -site-date-timezone {supported.timezone} {site.url}
```

Example:

```
gp stack php -site-date-timezone Pacific/Honolulu gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the timezone for your individual sites in your customizer here:

back to top ▲

▲

### Set the socket/stream wait timeout for a site’s PHP script.

The socket/stream wait time is not included in PHPs max execution time. The default socket timeout in PHP is 60 seconds. HTTP requests performed with some functions may exceed the execution time due to this wait being too short. Examples of such functions include:

file_get_contents, fopen or curl

Directive: default_socket_timeoutUnit: SecondsDefault value: 60

```
gp stack php -site-default-socket-timeout {integer} {site.url}
```

Example:

```
gp stack php -site-default-socket-timeout 300 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the default socket timeout for your individual sites in the site customizer here:

back to top ▲

▲

### Set the maximum execution time for a site’s PHP script.

Set the maximum time in seconds a site’s PHP script is allowed to run before it is terminated by the parser.

Directive: max_execution_timeUnit: SecondsDefault value: 300

```
gp stack php -site-max-exec-time {integer} {site.url}
```

Example:

```
gp stack php -site-max-exec-time 300 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the max execution time for your individual sites here:

back to top ▲

▲

### Set the maximum number of files that can be upload via a single request by a site’s PHP script.

The maximum number of files allowed to be uploaded simultaneously. Upload fields left blank on submission do not count towards this limit.

Directive: max_files_uploadUnit: FilesDefault value: 20

```
gp stack php -site-max-file-uploads {integer} {site.url}
```

Example:

```
gp stack php -site-upload-max-filesize 1024 {site.url}
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum number of files that can be uploaded for your individual sites inside your site customizer here:

back to top ▲

▲

### Set the maximum input time for a site’s PHP script.

Set the maximum time in seconds a site’s PHP script is allowed to parse input data, like POST and GET. Timing begins at the moment PHP is invoked at the server and ends when execution begins. Set to 0 to allow unlimited time.

Directive: max_input_timeUnit: SecondsDefault value: 60

```
gp stack php -site-max-input-time {integer} {site.url}
```

Example:

```
gp stack php -site-max-input-time 120 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum input time for your individual sites inside your customizer here:

back to top ▲

▲

### Set how many GET/POST/COOKIE input variables may be accepted by a site’s PHP script.

How many input variables may be accepted (limit is applied to $_GET, $_POST and $_COOKIE superglobal separately). Use of this directive mitigates the possibility of denial of service attacks that use hash collisions.

Directive: max_input_varsUnit: VariablesDefault value: 5000

```
gp stack php -site-max-input-vars {site.ur;} {site.url}
```

Example:

```
gp stack php -site-max-input-vars 10000 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the max input variables for your individual sites in your customizer here:

back to top ▲

▲

### Set the memory limit for a site’s PHP script

Set the maximum amount of memory that any site’s PHP script is allowed to allocate. This helps prevent poorly written scripts for eating up all available memory on a server. Note that to have no memory limit, set this directive to -1.

Directive: memory_limitUnit: MBDefault value: 256

```
gp stack php -site-mem-limit {integer} {site.url}
```

Example:

```
gp stack php -site-mem-limit 512 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the memory limit for each of your individual sites in your customizer here:

back to top ▲

▲

### Set the maximum post size per PHP script.

Sets max size of post data allowed.  To upload large files, this value must be larger than upload_max_filesize.  Generally speaking, this should also be smaller than the set memory_limit.

Directive: post_max_sizeUnit: MBDefault value: 512

```
gp stack php -site-post-max-size {integer} {site.url}
```

Example:

```
gp stack php -site-post-max-size 1024 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum post size for your individual sites in your customizer here:

back to top ▲

▲

### Set the session cookie lifetime for a cookie created by a site’s PHP script.

Specify the lifetime of a cookie in seconds which is sent to the browser. The value 0 means “until the browser is closed.”

Directive: session.cookie_lifetimeUnit: SecondsDefault value: 0

```
gp stack php -site-session-cookie-lifetime {integer} {site.url}
```

Example:

```
gp stack php -site-session-cookie-lifetime 3600 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

You can set the session cookie lifetime for your individual sites in your customizer here:

back to top ▲

▲

### Set the garbage collection for data created by a site’s PHP script.

Specify the number of seconds after which data will be seen as ‘garbage’ and potentially cleaned up.

Directive: session.gc_maxlifetimeUnit: SecondsDefault value: 1440

```
gp stack php -site-session-gc-maxlifetime {integer} {site.url}
```

Example:

```
gp stack php -site-session-gc-maxlifetime 3600 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

You can set the garbage collection lifetime for your individual sites in your site customizer here:

back to top ▲

▲

### Enable the short form of PHP’s open tag.

Tells PHP whether the short form <? ?> of PHP’s open tag should be allowed. Disabled by default, so it is possible to use PHP in combination with XML inline <? xml ?>. If you enable this option and have difficulties with xml inline, please remember to echo the XML'; ?>.

Directive: short_open_tagAccepted values: on | offDefault value: off

```
gp stack php -site-short-open-tag {on.off} {site.url}
```

Example:

```
gp stack php -site-short-open-tag on gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can enable PHP’s short open tag for your individual websites with this toggle inside your site customizer:

back to top ▲

▲

### Set the maximum upload file size a site’s PHP script allows.

Set the maximum size allowed for an uploaded file by a site’s PHP script.

Directive: upload_max_filesizeUnit: MBDefault value: 512

```
gp stack php -site-upload-max-filesize {integer} {site.url}
```

Example:

```
gp stack php -site-upload-max-filesize 1024 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum upload file size for your individual sites in your customizer here:

back to top ▲

▲

 

## Site PHP General Settings

These commands all take integer arguments, with the integer being converted into the required unit by the script. and impact all WordPress sites using that version of PHP.

You may notice many of these commands will configure the parameters identical to those at the PHP version level. As noted below each script that is affected, configuring these parameters at a site level will take precedence over the values set at the PHP version level.

▲

### Set The default timezone used by all date/time functions.

Sets The default timezone used by all date/time functions. The precedence order for which timezone is used if none is explicitly mentioned is described in the date_default_timezone_get() page at php.net. Please check this list of supported timezones at php.net.

Directive: date.timezoneDefault value: NULLAccepted Values: {supported.timezone} (String)

```
gp stack php -site-date-timezone {supported.timezone} {site.url}
```

Example:

```
gp stack php -site-date-timezone Pacific/Honolulu gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the timezone for your individual sites in your customizer here:

back to top ▲

▲

### Set the socket/stream wait timeout for a site’s PHP script.

The socket/stream wait time is not included in PHPs max execution time. The default socket timeout in PHP is 60 seconds. HTTP requests performed with some functions may exceed the execution time due to this wait being too short. Examples of such functions include:

file_get_contents, fopen or curl

Directive: default_socket_timeoutUnit: SecondsDefault value: 60

```
gp stack php -site-default-socket-timeout {integer} {site.url}
```

Example:

```
gp stack php -site-default-socket-timeout 300 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the default socket timeout for your individual sites in the site customizer here:

back to top ▲

▲

### Set the maximum execution time for a site’s PHP script.

Set the maximum time in seconds a site’s PHP script is allowed to run before it is terminated by the parser.

Directive: max_execution_timeUnit: SecondsDefault value: 300

```
gp stack php -site-max-exec-time {integer} {site.url}
```

Example:

```
gp stack php -site-max-exec-time 300 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the max execution time for your individual sites here:

back to top ▲

▲

### Set the maximum number of files that can be upload via a single request by a site’s PHP script.

The maximum number of files allowed to be uploaded simultaneously. Upload fields left blank on submission do not count towards this limit.

Directive: max_files_uploadUnit: FilesDefault value: 20

```
gp stack php -site-max-file-uploads {integer} {site.url}
```

Example:

```
gp stack php -site-upload-max-filesize 1024 {site.url}
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum number of files that can be uploaded for your individual sites inside your site customizer here:

back to top ▲

▲

### Set the maximum input time for a site’s PHP script.

Set the maximum time in seconds a site’s PHP script is allowed to parse input data, like POST and GET. Timing begins at the moment PHP is invoked at the server and ends when execution begins. Set to 0 to allow unlimited time.

Directive: max_input_timeUnit: SecondsDefault value: 60

```
gp stack php -site-max-input-time {integer} {site.url}
```

Example:

```
gp stack php -site-max-input-time 120 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum input time for your individual sites inside your customizer here:

back to top ▲

▲

### Set how many GET/POST/COOKIE input variables may be accepted by a site’s PHP script.

How many input variables may be accepted (limit is applied to $_GET, $_POST and $_COOKIE superglobal separately). Use of this directive mitigates the possibility of denial of service attacks that use hash collisions.

Directive: max_input_varsUnit: VariablesDefault value: 5000

```
gp stack php -site-max-input-vars {site.ur;} {site.url}
```

Example:

```
gp stack php -site-max-input-vars 10000 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the max input variables for your individual sites in your customizer here:

back to top ▲

▲

### Set the memory limit for a site’s PHP script

Set the maximum amount of memory that any site’s PHP script is allowed to allocate. This helps prevent poorly written scripts for eating up all available memory on a server. Note that to have no memory limit, set this directive to -1.

Directive: memory_limitUnit: MBDefault value: 256

```
gp stack php -site-mem-limit {integer} {site.url}
```

Example:

```
gp stack php -site-mem-limit 512 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the memory limit for each of your individual sites in your customizer here:

back to top ▲

▲

### Set the maximum post size per PHP script.

Sets max size of post data allowed.  To upload large files, this value must be larger than upload_max_filesize.  Generally speaking, this should also be smaller than the set memory_limit.

Directive: post_max_sizeUnit: MBDefault value: 512

```
gp stack php -site-post-max-size {integer} {site.url}
```

Example:

```
gp stack php -site-post-max-size 1024 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum post size for your individual sites in your customizer here:

back to top ▲

▲

### Set the session cookie lifetime for a cookie created by a site’s PHP script.

Specify the lifetime of a cookie in seconds which is sent to the browser. The value 0 means “until the browser is closed.”

Directive: session.cookie_lifetimeUnit: SecondsDefault value: 0

```
gp stack php -site-session-cookie-lifetime {integer} {site.url}
```

Example:

```
gp stack php -site-session-cookie-lifetime 3600 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

You can set the session cookie lifetime for your individual sites in your customizer here:

back to top ▲

▲

### Set the garbage collection for data created by a site’s PHP script.

Specify the number of seconds after which data will be seen as ‘garbage’ and potentially cleaned up.

Directive: session.gc_maxlifetimeUnit: SecondsDefault value: 1440

```
gp stack php -site-session-gc-maxlifetime {integer} {site.url}
```

Example:

```
gp stack php -site-session-gc-maxlifetime 3600 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set on a per-site level. Any per-site configuration will supersede this configuration.

You can set the garbage collection lifetime for your individual sites in your site customizer here:

back to top ▲

▲

### Enable the short form of PHP’s open tag.

Tells PHP whether the short form <? ?> of PHP’s open tag should be allowed. Disabled by default, so it is possible to use PHP in combination with XML inline <? xml ?>. If you enable this option and have difficulties with xml inline, please remember to echo the XML'; ?>.

Directive: short_open_tagAccepted values: on | offDefault value: off

```
gp stack php -site-short-open-tag {on.off} {site.url}
```

Example:

```
gp stack php -site-short-open-tag on gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can enable PHP’s short open tag for your individual websites with this toggle inside your site customizer:

back to top ▲

▲

### Set the maximum upload file size a site’s PHP script allows.

Set the maximum size allowed for an uploaded file by a site’s PHP script.

Directive: upload_max_filesizeUnit: MBDefault value: 512

```
gp stack php -site-upload-max-filesize {integer} {site.url}
```

Example:

```
gp stack php -site-upload-max-filesize 1024 gridpane.com
```

Optional last flag: -no-reload

This directive may also be set at the PHP version level. This site level setting will take precedence over any PHP version level setting.

You can set the maximum upload file size for your individual sites in your customizer here:

back to top ▲

▲

 

## PHP by Site – Process Manager/Workers

These settings allow you to manipulate how your PHP workers behave per site. The PHP version of your site is automatically detected and settings created are stored in a PHP pool {site.url}.conf:

```
/etc/php/{php.version}/fpm/pool.d/{site.url}.conf.
```

It’s important to note, only the settings configured using gp-cli will persist when you change PHP versions of your site. Any other configurations added to this file manually will be lost when a site’s PHP version is changed. If you do manually edit these files, please make a copy so you can reapply any additional manually configured parameters again after a PHP version switch.

In each command below, substitute your site for {site.url}.

Each command automatically reloads the requisite PHP version for that site, however, if you are wishing to chain together several commands you may wish to use the -no-reload flag as the last argument. This will stop you from reloading PHP multiple times, after which you can reload PHP.

For example:

```
gp stack php -site-pm static gridpane.com -no-reload &&  
gp stack php-site-pm-max-children 20 gridpane.com -no-reload && 
gp php 7.4 reload
```

back to top ▲

▲

### Set the site’s PHP process manager type.

Here are three ways to make PHP work: ondemand, static, & dynamic.

Directive: pmDefault value: dynamicAccepted Values: ondemand / static / dynamic

```
gp stack php -site-pm {accepted.value} {site.url}
```

Example:

```
gp stack php -site-pm static gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can set this inside your sites customizer here:

back to top ▲

▲

### Configure the site’s Maximum PHP Workers – Ondemand / Static / Dynamic

The number of child processes to be created when pm is set to static and the maximum number of child processes when pm is set to dynamic or ondemand. This value sets the limit on the number of simultaneous requests that will be served.

Our defaults on newly created servers are 4 workers per CPU core. So for 2 core server, your defaults will be 8 workers (2 x 4), on a 4 core server, it would be 16 (4 x 4).

Directive: pm.max_childrenDefault value: 4 x CPU CoreAccepted Values: integer

```
gp stack php -site-pm-max-children {accepted.value} {site.url}
```

Example for a 2 CPU server:

```
gp stack php -site-pm-max-children 8 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

### Configure a site’s PHP process manager max requests

This command will allow you to set how many requests the PHP process can take before it is recycled. It can be useful if the app has a memory leak. The default value is 500. Use this command to change that value:

Directive: pm.max_requestsDefault value: 500Accepted Values: integer

```
gp stack php -site-pm-max-requests {integer} {site.url}
```

Example:

```
gp stack php-site-pm-max-requests 300 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

### Configure a site’s Dynamic PHP Maximum Spare Workers

Set the maximum number of children in ‘idle’ state (waiting to process) workers. If the number of ‘idle’ processes is greater than this number then some children will be killed.

Note: Used only when pm is set to dynamic and is mandatory.

Directive: pm.max_spare_serversDefault value: 1Accepted Values: integer

```
gp stack php -site-pm-max-spare-servers {accepted.value} {site.url}
```

Example:

```
gp stack php -site-pm-max-spare-servers 4 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

### Configure a site’s Dynamic PHP Minimum Spare Workers

Set the minimum number of children in ‘idle’ state (waiting to process) workers. If the number of ‘idle’ processes is less than this number then some children will be created.

Note: Used only when pm is set to dynamic and is mandatory.

Directive: pm.min_spare_serversDefault value: 1Accepted Values: integer

```
gp stack php -site-pm-min-spare-servers {accepted.value} {site.url}
```

Example:

```
gp stack php -site-pm-min-spare-servers 4 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

### Configure a site’s Ondemand PHP Idle Process Timeout

Set the number of seconds after which an idle process will be killed.

Note: Used only when pm is set to ondemand.

Directive: pm.process_idle_timeoutDefault value: 10Accepted Values: integer

```
gp stack php -site-pm-process-idle-timeout {integer} {site.url}
```

Example:

```
gp stack php -site-pm-process-idle-timeout 4 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

### Configure a site’s Dynamic PHP Starting Workers

Set the number of children created on startup when process management is set to Dynamic.

Note: Used only when pm is set to dynamic and is mandatory.

Directive: pm.start_serversDefault value: 1Accepted Values: integer

```
gp stack php -site-pm-start-servers {accepted.value} {site.url}
```

Example:

```
gp stack php -site-pm-start-servers 2 gridpane.com
```

Optional last flag: -no-reload

This directive can only be set at the site level. You can change this in your site customizer here:

back to top ▲

▲

## How Your Site PHP Workers… Work

The process manager will control the number of child processes.

### Static

If you choose static, then there will always be PHP workers in existence no matter whether the application is active or not. This results in a higher resource footprint but can lead to increased performance when resources are plentiful as there is no wasted time in spinning processes up or down. It is important to manage workers against resources such as PHP memory when choosing this mode.

Given PHP is single-threaded it is often recommended to run from 1-2x as many Static PHP workers as you have threads available.

For that reason, you’ll want to set a maximum number of workers at the same time. Because our default is 100 workers, if you choose static without also setting the maximum, you’ll likely bring your whole server down in a short period of time. (unless you have a monster server)

It’s useful to string them together to avoid forgetting. This example sets the workers to 8, sets the site to static, and then reloads PHP 7.4:

```
gp stack php -site-pm-max-children 8 gridpane.com -no-reload && 
gp stack php -site-pm static gridpane.com -no-reload && 
gp php 7.4 restart
```

### Dynamic

If you choose dynamic, then you will not only be setting the maximum number of workers, but you will also need to set the minimum and maximum number of idle workers. It’s also a good idea to set the starting servers which will set the number of servers active when PHP starts up – giving it time to adjust up or down as needed.

Again, it’s useful to string them together to avoid forgetting. This example sets the maximum number of workers to 30, with 20 as the starting number, 10 as minimum idle, and 20 as maximum idle.

```
gp stack php -site-pm-max-children 30 gridpane.com -no-reload && 
gp stack php -site-pm-start-servers 20 gridpane.com -no-reload && 
gp stack php -site-pm-min-spare-servers 10 gridpane.com -no-reload && 
gp stack php -site-pm-max-spare-servers 20 gridpane.com -no-reload && 
gp php 7.4 restart
```

### Ondemand

If you choose ondemand, then there can be no PHP processes, with the server just spinning them up when needed. In this mode, you can set the maximum number of workers, but it is also important to set the amount of time after which idle processes can be killed.

Once again, it’s useful to string them together to avoid forgetting. This example sets the maximum number of workers to 100, with the idle timeout to 10 seconds.

```
gp stack php -site-pm-max-children 100 gridpane.com -no-reload && 
gp stack php -site-pm-process-idle-timeout 10 gridpane.com -no-reload && 
gp php 7.4 restart
```

 

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1024'%20height='544'%20viewBox='0%200%201024%20544'%3E%3C/svg%3E)

## Further Reading

If you’d like to learn more about PHP workers we have an in-depth blog post that digs into the topic. You can check it out here:

PHP Workers and WordPress: A Guide for Better Performance

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

