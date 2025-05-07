# The wp-config.php Location at GridPane | GridPane

# The wp-config.php Location at GridPane

 

1 min read 

To keep your WordPress configuration file (wp-config.php) secure, at GridPane it’s stored one level above your websites /htdocs folder.

Your wp-config.php file contains your database username and password along with other information about your website. We keep it hidden and protected.

You can find it on your server here (site.url = your websites domain name):

```
/var/www/site.url/
```

This contains GridPane specific configurations and so if migrating over, you will need to ensure that a second wp-configs.php is copied across inside the /htdocs folder, and if there is, delete this one, and NOT the GridPane version.

To learn more about making edits to the wp-config.php file on your GridPane websites and/or about checking your sites after a migration, please see this article that covers migrations, cloning, and the custom user-configs.php file which you can edit and place your own configurations into:

Migrations, Cloning, and the WordPress Configuration File (wp-config.php)

### Backup wp-config.php

A backup of the site’s wp-config.php is stored in the following directory:

```
/opt/gridpane/site-configs
```

This file is generated on the initial site build. You can use this backup copy to restore wp-config.php file if it’s ever deleted by accident. You may need to edit it to match the current state of the site/server configuration.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

