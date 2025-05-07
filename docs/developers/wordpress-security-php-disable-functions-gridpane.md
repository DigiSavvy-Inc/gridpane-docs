# WordPress Security & PHP disable_functions | GridPane

# WordPress Security & PHP disable_functions

 

5 min read 

### Table of Contents

 

## Introduction

disable_functions is a feature in PHP that allows you to prevent certain functions from being used. At GridPane, this feature is utilized to help secure your WordPress websites and reduce your attack surface by preventing the execution of potentially risky PHP functions that could be exploited by attackers.

Our default settings restrict access to specific PHP functions that aren’t critical for the vast majority of websites. This proactive measure significantly minimizes the potential for attackers to exploit vulnerabilities within these functions and offers an essential layer of protection, shielding you from a multitude of potential attacks.

This article details our default disable_functions settings and how to modify them on Nginx and OpenLiteSpeed servers.

 

## Default disable_functions Settings

The following PHP functions are disabled by default for all WordPress websites:

 

```
pcntl_alarm,pcntl_fork,pcntl_waitpid,pcntl_wait,pcntl_wifexited,pcntl_wifstopped,pcntl_wifsignaled,pcntl_wifsignaled,pcntl_wifcontinued,pcntl_wexitstatus,pcntl_wtermsig,pcntl_wstopsig,pcntl_signal,pcntl_signal_get_handler,pcntl_signal_dispatch,pcntl_get_last_error,pcntl_strerror,pcntl_sigprocmask,pcntl_sigwaitinfo,pcntl_sigtimedwait,pcntl_exec,pcntl_getpriority,pcntl_setpriority,pcntl_async_signals,posix_ctermid,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix,_getppid,posix_getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_setpgid,posix_setsid,posix_setuid,posix_times,posix_ttyname,posix_uname,socket_accept,socket_bind,socket_clear_error,socket_close,socket_connect,socket_listen,socket_create_listen,socket_read,socket_create_pair,stream_socket_server,proc_open,proc_close,proc_nice,proc_terminate,dl,link,highlight_file,show_source,diskfreespace,disk_free_space,getmyuid,popen,escapeshellcmd,symlink,shell_exec,exec,system,passthru,
```

## Modify disable_functions on Nginx

On Nginx servers, our disable_functions settings are implemented through a custom include file. Its location depends on the version of PHP your website is using, but it can be found here (switch the X for your PHP version and site.url for your website URL):

```
/etc/php/8.X/fpm/pool.d/site.url.disable-functions.include
```

For example:

```
/etc/php/8.2/fpm/pool.d/yourwebsite.com.disable-functions.include
```

### Step 1. Open the file

Open the file with the following command, switching out the PHP version and website URL as detailed above:

```
nano /etc/php/8.X/fpm/pool.d/site.url.disable-functions.include
```

### Step 2. Edit and Save your changes

The contents of this file looks as follows:

```
php_admin_value[disable_functions] =pcntl_alarm,pcntl_fork,pcntl_waitpid,pcntl_wait,pcntl_wifexited,pcntl_wifstopped,pcntl_wifsignaled,pcntl_wifsignaled,pcntl_wifcontinued,pcntl_wexitstatus,pcntl_wtermsig,pcntl_wstopsig,pcntl_signal,pcntl_signal_get_handler,pcntl_signal_dispatch,pcntl_get_last_error,pcntl_strerror,pcntl_sigprocmask,pcntl_sigwaitinfo,pcntl_sigtimedwait,pcntl_exec,pcntl_getpriority,pcntl_setpriority,pcntl_async_signals,posix_ctermid,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix,_getppid,posix_getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_setpgid,posix_setsid,posix_setuid,posix_times,posix_ttyname,posix_uname,socket_accept,socket_bind,socket_clear_error,socket_close,socket_connect,socket_listen,socket_create_listen,socket_read,socket_create_pair,stream_socket_server,proc_open,proc_close,proc_nice,proc_terminate,dl,link,highlight_file,show_source,diskfreespace,disk_free_space,getmyuid,popen,escapeshellcmd,symlink,shell_exec,exec,system,passthru,
```

You can remove any functions that you do not want disabled by simply deleting them while ensuring that there is still a comma between the functions before and after.

Once you’ve made your edits, save the file with CTRL+O followed by Enter. Exit the file with CTRL+X.

### Step 3. Reload PHP

Now that you’ve edited the file, you need to reload PHP (the version your website is running on) in order for your changes to take effect. You can reload PHP with the following command:

```
gp php 8.X reload
```

For example:

```
gp php 8.2 reload
```

 

## Modify disable_functions on OpenLiteSpeed (OLS)

On OpenLiteSpeed servers, our disable_functions settings are implemented through a custom in INI file. Its location depends on the version of PHP your website is using, but it can be found here (switch the X for your PHP version and site.url for your website URL):

```
/usr/local/lsws/lsphp8X/etc/php/8.X/litespeed/site.url/99-disable-functions.ini
```

For example:

```
/usr/local/lsws/lsphp82/etc/php/8.2/litespeed/yourwebsite.com/99-disable-functions.ini
```

### Step 1. Open the file

Open the file with the following command, switching out the PHP version and website URL as detailed above:

```
nano /usr/local/lsws/lsphp8X/etc/php/8.X/litespeed/site.url/99-disable-functions.ini
```

### Step 2. Edit and Save your changes

The contents of this file looks as follows:

```
[PHP]disable_functions =pcntl_alarm,pcntl_fork,pcntl_waitpid,pcntl_wait,pcntl_wifexited,pcntl_wifstopped,pcntl_wifsignaled,pcntl_wifsignaled,pcntl_wifcontinued,pcntl_wexitstatus,pcntl_wtermsig,pcntl_wstopsig,pcntl_signal,pcntl_signal_get_handler,pcntl_signal_dispatch,pcntl_get_last_error,pcntl_strerror,pcntl_sigprocmask,pcntl_sigwaitinfo,pcntl_sigtimedwait,pcntl_exec,pcntl_getpriority,pcntl_setpriority,pcntl_async_signals,posix_ctermid,posix_getcwd,posix_getegid,posix_geteuid,posix_getgid,posix_getgrgid,posix_getgrnam,posix_getgroups,posix_getlogin,posix_getpgid,posix_getpgrp,posix_getpid,posix,_getppid,posix_getpwuid,posix_getrlimit,posix_getsid,posix_getuid,posix_isatty,posix_kill,posix_mkfifo,posix_setegid,posix_seteuid,posix_setgid,posix_setpgid,posix_setsid,posix_setuid,posix_times,posix_ttyname,posix_uname,socket_accept,socket_bind,socket_clear_error,socket_close,socket_connect,socket_listen,socket_create_listen,socket_read,socket_create_pair,stream_socket_server,proc_open,proc_close,proc_nice,proc_terminate,dl,link,highlight_file,show_source,diskfreespace,disk_free_space,getmyuid,popen,escapeshellcmd,symlink,shell_exec,exec,system,passthru,
```

You can remove any functions that you do not want disabled, by simply deleting them while ensuring that there is still a comma between the functions before and after.

Once you’ve made your edits, save the file with CTRL+O followed by Enter. Exit the file with CTRL+X.

### Step 3. Regenerate your vhconf

For your changes to take effect, you will need to generate your websites vhconf with the following command (replace “site.url” with your domain name):

```
gpols site site.url
```

For example:

```
gpols site yourwebsite.com
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

