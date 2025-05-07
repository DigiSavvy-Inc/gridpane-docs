# Service Management: MySQL | GridPane

# Service Management: MySQL

 

1 min readStop/Start MySQL

These commands stop and start MySQL. Run them separately.

```
gp mysql -stop
gp mysql -start
```

Restart/Reload MySQL

The restart and reload commands both issue a STOP and then START from one command. They are effectively interchangeable.

```
gp mysql -restart
gp mysql -reload
```

Get MySQL Password

Outputs the MySQL password for a specified system user.

For root user:

```
gp mysql -get-pass root
```

For the admin user:

```
gp mysql -get-pass admin
```

For a site db user:

```
gp mysql -get-pass {site.url}
```

( replacing {site.url} with your actual site url )

Login to MySQL console

Grabs the specific user password and logs in to MySQL console directly.

Log in as root user:

```
gp mysql -login root
```

Log in as admin user:

```
gp mysql -login admin
```

Log in as a site db user:

```
gp mysql -login {site.url}
```

( replacing {site.url} with your actual site url )

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

