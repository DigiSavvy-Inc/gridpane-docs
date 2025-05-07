# Service Management: PHP | GridPane

# Service Management: PHP

 

1 min read 

## NGINX

Stop/Start PHP

These commands stop and start PHP. Run them separately. You have to designate the version in the command.

```
gp php {php.version} -stop
gp php {php.version} -start
```

For example:

```
gp php 7.3 -stop
```

Restart PHP

The restart command issues both a STOP and START command all in one. You have to designate the version in the command.

```
gp php {php.version} -restart
```

For example:

```
gp php 7.3 -restart
```

Reload PHP

Reload reloads the configuration without completely stopping the service. You have to designate the version in the command.

```
gp php {php.version} -reload
```

For example:

```
gp php 7.3 -reload
```

## OPENLITESPEED

Openlitespeed uses LSAPI instead of FPM version of PHP with their own LSPHP packages.In order to restart all PHP processes gracefully, you need to create a temporary file and restart Openlitespeed.

Run this to create a temporary file that tells OLS to restart all PHP process on next graceful restart

```
touch /usr/local/lsws/admin/tmp/.lsphp_restart.txt
```

Restart Openlitespeed

```
systemctl restart lsws
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

