# What are those weird extra sites inside /var/www? | GridPane

# What are those weird extra sites inside /var/www?

 

1 min read 

A fairly common question we get asked is “What are those two weird-looking sites on my server?”

Inside your servers /var/www directory, you can list all of your websites with:

```
ls -l
```

Here you’ll find two websites with a random set of letters and numbers as the subdomain of gridpanevps.com, for example:

```
22222
gy96dzepe0.gridpanevps.comgy96dzepe0stat.gridpanevps.com
```

These two sites, plus “22222”, are your servers Monit and PHPMyAdmin. They’re very important and take up very little space.

Please don’t delete them 🙂

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

