# Configure Nginx | GridPane

# Configure Nginx

 

36 min read 

# Index

### Enable Nginx Modules

### Configure Nginx Directives Serverwide

### GeoIP2 Configurations

Worker Configurations

Server Name Configurations

Limits Configurations

Open File Cache Configurations

FastCGI Configurations

Proxy Configurations

### Configure Nginx Per Site

Limits Configurations

FastCGI Configurations

Proxy Configurations

Redis SRCache Configurations

▲

# Enable Nginx Modules

Nginx has the ability to add new functionality through its use of modules. There is a huge range of core developed and community developed modules to enhance Nginx. Some of these modules are dynamic and can be enabled and disabled as needed.

back to top ▲

▲

# GeoIP2 Module

The ngx_http_geoip2_module creates variables with values from the maxmind geoip2 databases based on the client IP (default) or from a specific variable (supports both IPv4 and IPv6). Using this module you can easily filter traffic by a clients GeoIP based on country or city. Find out more here.

The GeoIp2 module makes use of the free GeoLite2 databases that are available from Maxminds website. Due to recent privacy changes all users must sign up for their own account to download and update these databases, GridPane can no longer distribute versions downloaded from our account. You can sign up for your account here.

Directive: load_moduleConfig location: /etc/nginx/nginx.confModule location: /etc/nginx/modules/ngx_http_geoip2_module.soModule location: /etc/nginx/modules/ngx_stream_geoip2_module.soContext: MainDefault state: offAccepted values: on | offRequired to enable: Maxmind AccountID + Maxmind License Key

```
gp stack nginx geoip -on {account.id}:{license.key}
gp stack nginx geoip -off
```

Example:

```
gp stack nginx geoip -on 57679:sd8Hj7kl
```

The Maxmind account information is only required when you first enable GeoIP2. We autogenerate a maxmind config at /etc/GeoIP.conf and store your account details in the server ENV so any subsequent reenabling can use these stored values. The account details allow the maxmind databases to be updated by a weekly cron.

back to top ▲

▲

# Configure Nginx Serverwide

These changes affect Nginx directives set in the main context, events context or http context, either directly in the nginx.conf or one of the direct includes to that file. As such these cli commands will make changes that apply to all sites on the server, unless an adjustment has been made to the same directive (if allowed) at a virtual server level specific to a site.

```
/etc/nginx/nginx.conf
```

Commands do not automatically reload their changes into Nginx. You will need to run a reload command after making any change. We do not recommend automatically reloading Nginx after any change without first checking Nginx syntax for any errors. To run an Nginx syntax check run:

```
nginx -t
```

Assuming everything is correct and the syntax check passes, reload Nginx using the gp-cli command to activate your changes:

```
gp ngx reload
```

back to top ▲

▲

### GeoIP2 Configurations

▲

### Block/Allow countries by GeoIP2 using their ISO 3166-1 country code

Creates an Nginx mapping using the 2 letter ISO 3166-1 country codes like so:

```
map $geoip2_data_country_code $allowed_country
```

Countries are passed as a csv list of countries and their respective allowed state, yes or no with a colon delimiter. These are set in the extra.d geoip context conf file. We default to yes, so as standard it is only necessary to set those countries we wish to deny:

```
KP:no,GB:no
```

However you can pass default as a value, and change that to No, to only set countries you wish to accept:

```
default:no,US:yes,GB:yes
```

Directives: geoip,mapConfig location: /etc/nginx/common/geoip.confConfig location: /etc/nginx/extra.d/geoip-context.confContext: httpDefault value: yes | KP no

```
gp stack nginx geoip -update {iso.code}:{yes.no},{iso.code}:{yes.no}
```

Example:

```
gp stack nginx geoip -update US:no,GB:no,FR:no
```

This directive may only be set in the http context and will always apply serverwide.

back to top ▲

▲

### Remove countries from GeoIP2 mapping using their ISO 3166-1 country code

Removes countries from the following GeoIP2 mapping:

```
map $geoip2_data_country_code $allowed_country
```

Countries are passed as a csv list of countries using their 2 letter ISO 3166-1 country code, they are then removed from the extra.d geoip context conf.

```
KP,GB,US
```

Directives: geoip,mapConfig location: /etc/nginx/common/geoip.confConfig location: /etc/nginx/extra.d/geoip-context.confContext: http

```
gp stack nginx geoip -remove {iso.code},{iso.code},{iso.code}
```

Example:

```
gp stack nginx geoip -remove US,GB,FR
```

This directive may only be set in the http context and will always apply serverwide.

back to top ▲

▲

### Configure Nginx Workers

NGINX can run multiple worker processes, each capable of processing a large number of simultaneous connections. worker_processes is the number of NGINX worker processes. In most cases, running one worker process per CPU core works well, and we follow the recommended practice of setting this directive to auto which achieves that. You can control how your worker processes handle workloads with the following directives.

back to top ▲

▲

### Sets the maximum number of simultaneous connections that can be opened by a worker process.

Sets the maximum number of simultaneous connections that can be opened by a worker process. It should be kept in mind that this number includes all connections (e.g. connections with proxied servers, among others), not only connections with clients. Another consideration is that the actual number of simultaneous connections cannot exceed the current limit on the maximum number of open files, which can be changed by worker_rlimit_nofile.

Directive: worker_connectionsConfig location: /etc/nginx/nginx.confContext: eventsDefault value: 8192

```
gp stack nginx worker -connections {integer}
```

Example:

```
gp stack nginx worker -connections 4096
```

This directive may only be set in the events context and will always apply serverwide.

back to top ▲

▲

### Change the maximum number of possible open files for worker processes

Changes the limit on the maximum number of open files (RLIMIT_NOFILE) for worker processes. Used to increase the limit without restarting the main process. We default to setting this high.

Directive: worker_rlimit_nofileConfig location: /etc/nginx/nginx.confContext: mainDefault value: Set at server provision based on available RAM

```
gp stack nginx worker -rlimit-nofile {integer}
```

Example:

```
gp stack nginx worker -rlimit-nofile 789022
```

This directive may only be set in the main context and will always apply serverwide.

back to top ▲

▲

### Server Name Configurations

The following directives will affect how Nginx processes the server_name directive upon receiving requests.

back to top ▲

▲

### Enables/disable the use of the primary server name in absolute redirects

Enables or disables the use of the primary server name, specified by the server_name directive, in absolute redirects issued by nginx. Disabling server_name_in_redirects makes sure the server_name (specified in each site’s virtual server block) is not used in redirects. It will instead use the name specified in the Host request header field. We default to this more secure implementation.

Directive: server_name_in_redirectConfig location: /etc/nginx/common/basics.confDefault value: offAccepted values: on | off

To enable:

```
gp stack nginx server-name -in-redirect {accepted.value}
```

Example:

```
gp stack nginx server-name -in-redirect on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the bucket size for the server names hash tables

Sets the bucket size for the server names hash tables.

Directive: server_name_hash_bucket_sizeConfig location: /etc/nginx/nginx.confContext: httpDefault value: 256Accepted values: integer memory values – 64|128|256|512 etc

```
gp stack nginx server-name -hash-bucket-size {accepted.integer}
```

Example:

```
gp stack nginx server-name -hash-bucket-size 512
```

This directive may only be set in the http context and will always apply serverwide.

back to top ▲

▲

### Limits Configurations

The following directives will set different limits for a variety of Nginx features.

back to top ▲

▲

### Sets buffer size for reading client request body

Sets buffer size for reading client request body. In case the request body is larger than the buffer, the whole body or only its part is written to a temporary file.

Directive: client_body_buffer_sizeConfig location: /etc/nginx/common/limits.confContext: httpUnit: KBDefault value: 128Accepted values: integers

```
gp stack nginx limits -client-body-buffer-size {accepted.integer}
```

Example:

```
gp stack nginx limits -client-body-buffer-size 64
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for reading client request body.

Defines a timeout for reading client request body. The timeout is set only for a period between two successive read operations, not for the transmission of the whole request body. If a client does not transmit anything within this time, the request is terminated with the 408 (Request Time-out) error.

Directive: client_body_timeoutConfig location: /etc/nginx/common/limits.confContext: httpUnit: SecondsDefault value: 30Accepted values: integers

```
gp stack nginx limits -client-body-timeout {accepted.integer}
```

Example:

```
gp stack nginx limits -client-body-timeout 60
```

This directive may also be adjusted in the server context, to be applied on a site by site basis. You will need to do this manually using an include.

back to top ▲

▲

### Sets buffer size for reading client request header

Sets buffer size for reading client request header. If a request line or a request header field does not fit into this buffer then larger buffers, configured by the large_client_header_buffers directive, are allocated.

Directive: client_header_buffer_sizeConfig location: /etc/nginx/common/limits.confContext: httpUnit: KBDefault value: 13Accepted values: integers

```
gp stack nginx limits -client-header-buffer-size {accepted.integer}
```

Example:

```
gp stack nginx limits -client-header-buffer-size 4
```

This directive may also be adjusted in the server context, to be applied on a site by site basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for reading client request header.

Defines a timeout for reading client request header. If a client does not transmit the entire header within this time, the request is terminated with the 408 (Request Time-out) error.

Directive: client_header_timeoutConfig location: /etc/nginx/common/limits.confContext: httpUnit: SecondsDefault value: 30Accepted values: integers

```
gp stack nginx limits -client-header-timeout {accepted.integer}
```

Example:

```
gp stack nginx limits -client-header-timeout 60
```

This directive may also be adjusted in the server context, to be applied on a site by site basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the maximum number of requests that can be served through one keep-alive connection

Sets the maximum number of requests that can be served through one keep-alive connection. After the maximum number of requests are made, the connection is closed. Closing connections periodically is necessary to free per-connection memory allocations.

Directive: keepalive_requestsConfig location: /etc/nginx/common/limits.confContext: httpDefault value: 5000Accepted values: integers

```
gp stack nginx limits -keepalive-requests {accepted.integer}
```

Example:

```
gp stack nginx limits -keepalive-requests 500
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set a timeout during which a keep-alive client connection will stay open on the server side.

Sets a timeout during which a keep-alive client connection will stay open on the server side. The zero value disables keep-alive client connections. An optional second parameter can be added to set a value in the “Keep-Alive: timeout=time” response header field. Two parameters may differ. This would need to be done manually.

Directive: keepalive_timeoutConfig location: /etc/nginx/common/limits.confContext: httpUnit: SecondsDefault value: 30Accepted values: integers

```
gp stack nginx limits -keepalive-timeout {accepted.integer}
```

Example:

```
gp stack nginx limits -keepalive-timeout 60
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the maximum number and size of buffers used for reading large client request header.

Sets the maximum number and size of buffers used for reading large client request header. A request line cannot exceed the size of one buffer, or the 414 (Request-URI Too Large) error is returned to the client. A request header field cannot exceed the size of one buffer as well, or the 400 (Bad Request) error is returned to the client. Buffers are allocated only on demand. If after the end of request processing a connection is transitioned into the keep-alive state, these buffers are released.

Directive: large_client_header_buffersConfig location: /etc/nginx/common/limits.confContext: httpUnit: Buffer quantity and KB (buffer size)Default value: 4 52Accepted values: integers

```
gp stack nginx limits -large-client-header-buffers {b.quantity} {b.size}
```

Example:

```
gp stack nginx limits -large-client-header-buffers 8 28
```

This directive may also be adjusted in the server context, to be applied on a site by site basis. You will need to do this manually using an include.

back to top ▲

▲

### Set parameters for a shared memory zone to store the current number of excessive requests.

Sets parameters for a shared memory zone that will keep states for various keys. In particular, the state stores the current number of excessive requests. GridPane servers come with 2 preconfigured zones being used to limit requests to site urls:

It is usually not necessary to adjust these request rate, as a queue and burst rate can be adjusted on a per site basis to allow for heavier request rates that may be required by some plugins. Please adjust the specific zones limit_req using a site cli command to achieve this.

#### Zone One

Directive: limit_req_zoneConfig location: /etc/nginx/common/limits.confContext: httpUnit: MB (key store size) and Rate (requests/s)Default value: 10 3Accepted values: integers

```
gp stack nginx limits -req-zone-one {store.size.mb} {req.per.sec}
```

Example:

```
gp stack nginx limits -req-zone-one 5 2
```

#### Zone WP

Directive: limit_req_zoneConfig location: /etc/nginx/common/limits.confContext: httpUnit: MB (key store size) and Rate (requests/s)Default value: 10 3Accepted values: integers

```
gp stack nginx limits -req-zone-wp {store.size.mb} {req.per.sec}
```

Example:

```
gp stack nginx limits -req-zone-wp 15 6
```

back to top ▲

▲

### Enable/disable the resetting of timed out connections.

Enables or disables resetting timed out connections and connections closed with the non-standard code 444 (1.15.2). The reset is performed as follows. Before closing a socket, the SO_LINGER option is set on it with a timeout value of 0. When the socket is closed, TCP RST is sent to the client, and all memory occupied by this socket is released. This helps avoid keeping an already closed socket with filled buffers in a FIN_WAIT1 state for a long time.

It should be noted that timed out keep-alive connections are closed normally.

Directive: reset_timedout_connectionConfig location: /etc/nginx/common/limits.confContext: httpDefault value: onAccepted values: on | off

```
gp stack nginx limits -reset-timedout-connection {accepted.value}
```

Example:

```
gp stack nginx limits -reset-timedout-connection on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set a timeout for transmitting a response to the client.

Sets a timeout for transmitting a response to the client. The timeout is set only between two successive write operations, not for the transmission of the whole response. If the client does not receive anything within this time, the connection is closed.

Directive: send_timeoutConfig location: /etc/nginx/common/limits.confContext: httpUnit: SecondsDefault value: 60Accepted values: integer

```
gp stack nginx limits -send-timeout {accepted.value}
```

Example:

```
gp stack nginx limits -send-timeout 45
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the maximum size of the types hash tables.

Sets the maximum size of the types hash tables.

Directive: types_hash_max_sizeConfig location: /etc/nginx/common/limits.confContext: httpDefault value: 2048Accepted values: integer

```
gp stack nginx limits -types-hash-max-size {accepted.value}
```

Example:

```
gp stack nginx limits -types-hash-max-size 1024
```

This directive may also be adjusted in the server context, to be applied on a site by site basis. You will need to do this manually using an include.

back to top ▲

▲

### Open File Cache Configurations

The following directives will configure different aspects of the Nginx open file cache.

back to top ▲

▲

### Enable and configure the open file cache

Configures an nginx cache that can store:

Caching of errors should be enabled separately by the open_file_cache_errors directive. The directive has the following parameters:

Directive: open_file_cacheConfig location: /etc/nginx/common/limits.confContext: httpUnits: Files (max.elements) Seconds (inactive.timeout) Default values: 5000 60Accepted values: integer

```
gp stack nginx open-file-cache -max {elements} -inactive {timeout}
```

Example:

```
gp stack nginx open-file-cache -max 1000 -inactive 60
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Enable/disables the caching of file lookup errors by the open file cache.

Enables or disables caching of file lookup errors by open_file_cache.

Directive: open_file_cache_errorsConfig location: /etc/nginx/common/limits.confContext: httpDefault values: offAccepted values: on | off

```
gp stack nginx open-file-cache -errors {accepted.value}
```

Example:

```
gp stack nginx open-file-cache -errors on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Sets the minimum number of file accesses during the period configured by the open file cache.

Sets the minimum number of file accesses during the period configured by the inactive parameter of the open_file_cache directive, required for a file descriptor to remain open in the cache.

Directive: open_file_cache_min_usesConfig location: /etc/nginx/common/limits.confContext: httpDefault value: 1Accepted values: integers

```
gp stack nginx open-file-cache -min-uses {accepted.value}
```

Example:

```
gp stack nginx open-file-cache -min-uses 2
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Sets a time after which open file cache elements should be revalidated.

Sets a time after which open_file_cache elements should be validated.

Directive: open_file_cache_validConfig location: /etc/nginx/common/limits.confContext: httpUnits: Seconds Default values: 60Accepted values: integer

```
gp stack nginx open-file-cache -valid {accepted.value}
```

Example:

```
gp stack nginx open-file-cache -valid 120
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### FastCGI Configurations

GridPane uses Nginx with FastCGI proxying to process client PHP requests by proxying them to a PHP-FPM server for processing. FastCGI is a protocol based on the earlier CGI, or common gateway interface, protocol that greatly improves performance by not running each request as a separate process.

The directive that Nginx uses to define the actual server to proxy to using the FastCGI protocol is fastcgi_pass. The primary method of passing extra information when using the FastCGI protocol is with parameters,  using the fastcgi_param directive.

Fastcgi directives are configured in the following file:

```
/etc/nginx/conf.d/fastcgi.conf
```

Fastcgi parameters are configured in the following file:

```
/etc/nginx/fastcgi_params
```

The following directives will configure different aspects of the fastcgi proxying process and its management.

back to top ▲

▲

### Enable/disable buffering of responses from the FastCGI server.

Enables or disables buffering of responses from the FastCGI server. When buffering is enabled, nginx receives a response from the FastCGI server as soon as possible, saving it into the buffers set by the fastcgi_buffer_size and fastcgi_buffers directives.

When buffering is disabled, the response is passed to a client synchronously, immediately as it is received. nginx will not try to read the whole response from the FastCGI server. The maximum size of the data that nginx can receive from the server at a time is set by the fastcgi_buffer_size directive.

Directive: fastcgi_bufferingConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx fastcgi -buffering {accepted.value}
```

Example:

```
gp stack nginx fastcgi -buffering off
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the number and size of buffers used for reading responses from the FastCGI server.

Sets the number and size of the buffers used for reading a response from the FastCGI server, for a single connection.

Directive: fastcgi_buffersConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnits: Number (buffer.quantity) K (buffer.size)Default values: 8 64Accepted values: integers

```
gp stack nginx fastcgi -buffers {b.quantity} {b.size}
```

Example:

```
gp stack nginx fastcgi -buffers 8 16
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the buffer size used for reading the first part of the response from the FastCGI server.

Sets the size of the buffer used for reading the first part of the response received from the FastCGI server. This part usually contains a small response header.

Directive: fastcgi_buffer_sizeConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnits: KDefault values: 128Accepted values: integer

```
gp stack nginx fastcgi -buffer-size {accepted.value}
```

Example:

```
gp stack nginx fastcgi -buffer-size 16
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Limit the total size of buffers that can be busy sending a response to the client while the response is not yet fully read.

When buffering of responses from the FastCGI server is enabled, limits the total size of buffers that can be busy sending a response to the client while the response is not yet fully read. In the meantime, the rest of the buffers can be used for reading the response and, if needed, buffering part of the response to a temporary file.

Directive: fastcgi_busy_buffers_sizeConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnits: KDefault values: 256Accepted values: integer

```
gp stack nginx fastcgi -busy-buffers-size {accepted.value}
```

Example:

```
gp stack nginx fastcgi -busy-buffers-size 64
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Update FastCGI cache in background while stale response is served.

Allows starting a background subrequest to update an expired cache item, while a stale cached response is returned to the client. Note that it is necessary to allow the usage of a stale cached response when it is being updated, we do this by using the fastcgi_cache_use_stale updating; directive. It can also be enabled using the Cache-control: stale-* headers.

Directive: fastcgi_cache_background_updateConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx fastcgi -cache-background-update {accepted.value}
```

Example:

```
gp stack nginx fastcgi -cache-background-update off
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the maximum size of the FastCGI cache in RAM

Define the maximum amount of RAM to be used by Nginx FastCGI Caching. Sets the max_size parameter of the fastcgi_cache_path directive.

Directive: fastcgi_cache_path max_sizeConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnit: MB Accepted value: Integer

```
gp stack nginx fastcgi -max-cache-size {accepted.value}
```

Example:

```
gp stack nginx fastcgi -max-cache-size 512
```

back to top ▲

▲

### Enable revalidation of expired cache items using conditional requests

Enables revalidation of expired cache items using conditional requests with the If-Modified-Since and If-None-Match header fields.

Directive: fastcgi_cache_revalidateConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx fastcgi -cache-revalidate {accepted.value}
```

Example:

```
gp stack nginx fastcgi -cache-revalidate off
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Defines a timeout for establishing a connection with a FastCGI server.

Defines a timeout for establishing a connection with a FastCGI server. It should be noted that this timeout cannot usually exceed 75 seconds.

Directive: fastcgi_connect_timeoutConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnit: SecondsDefault values: 60Accepted values: 1 – 75

```
gp stack nginx fastcgi -connect-timeout {accepted.value}
```

Example:

```
gp stack nginx fastcgi -connect-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Instruct the FastCGI server to keep connnections open to Nginx.

By default, a FastCGI server will close a connection right after sending the response. However, when this directive is set to the value on, nginx will instruct a FastCGI server to keep connections open. This is necessary, in particular, for keepalive connections to FastCGI servers to function.

Directive: fastcgi_keep_connConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx fastcgi -keep-connections {accepted.value}
```

Example:

```
gp stack nginx fastcgi -keep-connections on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for reading a response from the FastCGI server.

Defines a timeout for reading a response from the FastCGI server. The timeout is set only between two successive read operations, not for the transmission of the whole response. If the FastCGI server does not transmit anything within this time, the connection is closed.

Directive: fastcgi_read_timeoutConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnit: SecondsDefault value: 60Accepted value: Integer

```
gp stack nginx fastcgi -read-timeout {accepted.value}
```

Example:

```
gp stack nginx fastcgi -read-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for transmitting a request to the FastCGI server.

Sets a timeout for transmitting a request to the FastCGI server. The timeout is set only between two successive write operations, not for the transmission of the whole request. If the FastCGI server does not receive anything within this time, the connection is closed.

Directive: fastcgi_send_timeoutConfig location: /etc/nginx/conf.d/fastcgi.confContext: httpUnit: SecondsDefault value: 60Accepted value: Integer

```
gp stack nginx fastcgi -send-timeout {accepted.value}
```

Example:

```
gp stack nginx fastcgi -send-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Proxy Configurations

Nginx can be set up in a reverse proxy configuration that will allow an Nginx server to sit infront of another webserver and request will be passed from Nginx to the other webserver. This configuration is usually reserved for fusion stacks that have Nginx sitting infront of Apache2 or working as a load balancer. However at GridPane we use this configuration for any sites where the ModSec firewall is enabled. We run Nginx as a caching reverse proxy infront of an Nginx FastCGI instance that is filtering request through the ModSec firewall. This vastly increases the performance of sites running the ModSec firewall by only filtering requests that miss the cache, as recommended by TrustWave.

The directive that Nginx uses to define the actual server to proxy to is proxy_pass.Proxy directives are configured in the following file:

```
/etc/nginx/conf.d/proxy.conf
```

The following directives will configure different aspects of the Nginx caching reverse proxy and its management.

back to top ▲

▲

### Enable/disable buffering of responses from the Proxy server.

Enables or disables buffering of responses from the Proxy server. When buffering is enabled, nginx receives a response from the Proxy server as soon as possible, saving it into the buffers set by the proxy_buffer_size and proxy_buffers directives.

When buffering is disabled, the response is passed to a client synchronously, immediately as it is received. nginx will not try to read the whole response from the Proxy server. The maximum size of the data that nginx can receive from the server at a time is set by the proxy_buffer_sizecode> directive.

Directive: proxy_bufferingConfig location: /etc/nginx/conf.d/proxy.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx proxy -buffering {accepted.value}
```

Example:

```
gp stack nginx proxy -buffering off
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the number and size of buffers used for reading responses from the proxy server.

Sets the number and size of the buffers used for reading a response from the proxy server, for a single connection.

Directive: proxy_buffersConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnits: Number (buffer.quantity) K (buffer.size)Default values: 8 64Accepted values: integers

```
gp stack nginx proxy -buffers {b.quantity} {b.size}
```

Example:

```
gp stack nginx proxy -buffers 8 16
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the buffer size used for reading the first part of the response from the proxy server.

Sets the size of the buffer used for reading the first part of the response received from the proxy server. This part usually contains a small response header.

Directive: proxy_buffer_sizeConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnits: KDefault values: 128Accepted values: integer

```
gp stack nginx proxy -buffer-size {accepted.value}
```

Example:

```
gp stack nginx proxy -buffer-size 16
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Limit the total size of buffers that can be busy sending a response to the client while the response is not yet fully read.

When buffering of responses from the proxy server is enabled, limits the total size of buffers that can be busy sending a response to the client while the response is not yet fully read. In the meantime, the rest of the buffers can be used for reading the response and, if needed, buffering part of the response to a temporary file.

Directive: proxy_busy_buffers_sizeConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnits: KDefault values: 256Accepted values: integer

```
gp stack nginx proxy -busy-buffers-size {accepted.value}
```

Example:

```
gp stack nginx proxy -busy-buffers-size 64
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Update proxy cache in background while stale response is served.

Allows starting a background subrequest to update an expired cache item, while a stale cached response is returned to the client. Note that it is necessary to allow the usage of a stale cached response when it is being updated, we do this by using the proxy_cache_use_stale updating; directive. It can also be enabled using the Cache-control: stale-* headers.

Directive: proxy_cache_background_updateConfig location: /etc/nginx/conf.d/proxy.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx proxy -cache-background-update {accepted.value}
```

Example:

```
gp stack nginx proxy -cache-background-update off
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Set the maximum size of the proxy cache in RAM

Define the maximum amount of RAM to be used by Nginx Proxy Caching. Sets the max_size parameter of the proxy_cache_path directive.

Directive: proxy_cache_path max_sizeConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnit: MB Accepted value: Integer

```
gp stack nginx proxy -max-cache-size {accepted.value}
```

Example:

```
gp stack nginx proxy -max-cache-size 512
```

back to top ▲

▲

### Enables revalidation of expired cache items using conditional requests.

Enables revalidation of expired cache items using conditional requests with the If-Modified-Since and If-None-Match header fields.

Directive: proxy_cache_revalidateConfig location: /etc/nginx/conf.d/proxy.confContext: httpDefault values: offAccepted values: on | off

```
gp stack nginx proxy -cache-revalidate {accepted.value}
```

Example:

```
gp stack nginx proxy -cache-revalidate on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Defines a timeout for establishing a connection with a proxy server.

Defines a timeout for establishing a connection with a proxy server. It should be noted that this timeout cannot usually exceed 75 seconds.

Directive: proxy_connect_timeoutConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnit: SecondsDefault values: 60Accepted values: 1 – 75

```
gp stack nginx proxy -connect-timeout {accepted.value}
```

Example:

```
gp stack nginx proxy -connect-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Instruct the Proxied server to keep connnections open to Nginx.

By default, a proxy server will close a connection right after sending the response. However, when this directive is set to the value on, nginx will instruct a proxied server to keep connections open. This is necessary, in particular, for keepalive connections to proxy servers to function.

Directive: proxy_keep_connConfig location: /etc/nginx/conf.d/proxy.confContext: httpDefault values: onAccepted values: on | off

```
gp stack nginx proxy -keep-connections {accepted.value}
```

Example:

```
gp stack nginx proxy -keep-connections on
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for reading a response from the proxy server.

Defines a timeout for reading a response from the proxy server. The timeout is set only between two successive read operations, not for the transmission of the whole response. If the proxy server does not transmit anything within this time, the connection is closed.

Directive: proxy_read_timeoutConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnit: SecondsDefault value: 60Accepted value: Integer

```
gp stack nginx proxy -read-timeout {accepted.value}
```

Example:

```
gp stack nginx proxy -read-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Define a timeout for transmitting a request to the proxy server.

Sets a timeout for transmitting a request to the proxy server. The timeout is set only between two successive write operations, not for the transmission of the whole request. If the proxy server does not receive anything within this time, the connection is closed.

Directive: proxy_send_timeoutConfig location: /etc/nginx/conf.d/proxy.confContext: httpUnit: SecondsDefault value: 60Accepted value: Integer

```
gp stack nginx proxy -send-timeout {accepted.value}
```

Example:

```
gp stack nginx proxy -send-timeout 30
```

This directive may also be adjusted in the server and location contexts, to be applied on a site by site or location by location basis. You will need to do this manually using an include.

back to top ▲

▲

# Configure Nginx per Site

These changes affect Nginx directives set in the server context, either directly in site specific configurations files included into the sites virtual server. As such these cli commands will make changes only to individual sites.

Site virtual server files are located here:

```
/etc/nginx/sites-available/{site.url}
```

And symlinked into here to become active:

```
/etc/nginx/sites-available/{site.url}
```

Sites also have common configuration files that are found here:

```
/etc/nginx/common/{site.url}-{config-name}.conf
```

back to top ▲

▲

### Site Nginx Limits Configurations

The following directives will set different limits for a variety of Nginx features on a per site basis.

back to top ▲

▲

### Set the maximum burst size request queue for when a zone rate limit has been hit.

Sets the maximum burst size of requests to queue when a zone rate limit has been hit. If the requests rate exceeds the rate configured for a zone, a queue is created from the burst number and processed with nodelay. Any requests that exceed this rate limit and burst are dropped with a 503 error code.

#### Zone One

Directive: limit_reqConfig location: /etc/nginx/common/{site.url}-wpcommon.confContext: serverAccepted values: integer, fqdn

```
gp stack nginx limits -site-zone-one-burst {queue.size} {site.url}
```

Example:

```
gp stack nginx limits -site-zone-one-burst 1 gridpane.com
```

#### Zone WP

Directive: limit_reqConfig location: /etc/nginx/common/{site.url}-wpcommon.confContext: serverAccepted values: integer, fqdn

```
gp stack nginx limits -site-zone-wp-burst {queue.size} {site.url}
```

Example:

```
gp stack nginx limits -site-zone-wp-burst 20 gridpane.com
```

back to top ▲

▲

### Set the maximum allowed size of the client request body

Sets the maximum allowed size of the client request body, specified in the Content-Length request header field. If the size in a request exceeds the configured value, the 413 (Request Entity Too Large) error is returned to the client. Please be aware that browsers cannot correctly display this error. Setting size to 0 disables checking of client request body size.

Directive: client_max_body_sizeConfig location: /etc/nginx/common/{site.url}-wpcommon.confContext: serverUnit: MBDefault value: 512Accepted value: Integer

```
gp stack nginx limits -site-max-body-size {accepted.value} {site.url}
```

Example:

```
gp stack nginx limits -site-max-body-size 1024 gridpane.url
```

This directive may also be adjusted in the location context, to be applied on a location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Site FastCGI Configurations

The following directives will adjust Fastcgi settings on a site per site basis.

back to top ▲

▲

### Sets caching expiry time for all successful requests going into FastCGI cache.

Sets caching time for all requests that return a 200 success code on a per site basis.

Directive: fastcgi_cache_validConfig location: /etc/nginx/common/{site.url}-fcgi-cache-var.confContext: serverUnit: SecondsDefault value: 1Accepted value: Integer

```
gp stack nginx fastcgi -site-cache-valid {accepted.value} {site.url}
```

Example:

```
gp stack nginx fastcgi -site-cache-valid 1800 gridpane.url
```

This directive may also be adjusted in the location context, to be applied on a location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Site Proxy Configurations

The following directives will adjust Proxy settings on a site per site basis.

back to top ▲

▲

### Sets caching expiry time for all successful requests going into Proxy cache.

Sets caching time for all requests that return a 200 success code on a per site basis.

Directive: proxy_cache_validConfig location: /etc/nginx/common/{site.url}-proxy-cache-var.confContext: serverUnit: SecondsDefault value: 1Accepted value: Integer

```
gp stack nginx proxy -site-cache-valid {accepted.value} {site.url}
```

Example:

```
gp stack nginx proxy -site-cache-valid 1800 gridpane.com
```

This directive may also be adjusted in the location context, to be applied on a location by location basis. You will need to do this manually using an include.

back to top ▲

▲

### Sets caching expiry time for all successful requests going into Redis SRCache page cache.

Sets caching time for all requests that return a 200 success code on a per site basis.

Directive: redis2_query expire $key $cache_ttlConfig location: /etc/nginx/common/{site.url}-wp-redis.confConfig location: /etc/nginx/common/{site.url}-proxy-http-rediscache.confConfig location: /etc/nginx/common/{site.url}-proxy-https-rediscache.confContext: serverUnit: SecondsDefault value: 2592000Accepted value: Integer

```
gp stack nginx redis -site-cache-valid {accepted.value} {site.url}
```

Example:

```
gp stack nginx redis -site-cache-valid 1200000 gridpane.com
```

This directive may also be adjusted in the location context, to be applied on a location by location basis. You will need to do this manually using an include.

back to top ▲

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

