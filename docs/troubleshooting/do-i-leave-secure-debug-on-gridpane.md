# Do I Leave Secure Debug On? | GridPane

# Do I Leave Secure Debug On?

 

1 min read 

To keep the contents secure, GridPane has a custom Secure Debug log which takes the default WordPress debug log and places it in the domain root one level above the htdocs directory.

## Should you leave Secure Debug On?

No.

Secure debug is a handy tool for actively debugging WordPress issues. However, once you’ve completed your debug you should deactivate it.

Leaving it active unnecessarily has the potential to create a log file that becomes huge in size, especially if you have errors or warnings firing regularly. This can cause disk space issues on smaller servers.

## Activation/Deactivation

To enable Secure Debug, toggle the switch in the site configuration modal. That will create two files:

```
/var/www/site.url/secure-debug.php
 /var/www/site.url/logs/debug.log
```

The secure-debug.php file pulls data in from the log and displays it on the dashboard.

When done debugging, toggle it back off.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

