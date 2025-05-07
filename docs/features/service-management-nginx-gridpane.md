# Service Management: Nginx | GridPane

# Service Management: Nginx

 

1 min readNginx Configuration Check

Run either of these commands after making configuration changes to find issues before reloading or restarting the Nginx.

```
gp ngx -t
gp ngx -status
```

Stop/Start Nginx

These commands stop and start Nginx. Run them separately.

```
gp ngx -stop
gp ngx -start
```

Restart Nginx

The restart command issues a STOP and then START from one command.

```
gp ngx -restart
```

Reload Nginx

Reload reloads the configuration without completely stopping the service. Specifically, RELOAD will do the following:

```
gp ngx -reload
```

In addition the GridPane Nginx reload command will initiate an OCSP stapling response request for all domain configurations with SSL to avoid issues related to Nginx of “lazy loading” responses after the first request.

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

