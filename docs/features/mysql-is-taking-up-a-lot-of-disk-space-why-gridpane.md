# MySQL is taking up a LOT of disk space. Why? | GridPane

# MySQL is taking up a LOT of disk space. Why?

 

1 min readIf you’re finding that your MySQL is taking up a large amount of disk space on your servers, and you’re not running any particularly large websites, it’s likely that this is due to how InnoDB works.

What may be happening is your sites are storing a lot of temporary data inside the database. Each InnoDB table is stored in it’s own file, and InnoDB files can grow, but not shrink on their own. So even though you might have a huge InnoDB file, it may only have 200Mb of real data inside it.

There are 2 ways to fix this: –

The WP CLI Method

To run a database optimization with WP CLI, first connect to your server using SSH. Here are our articles on how to do this: –

Generate SSH Key on Mac

Generate SSH Key on Windows with Putty

Generate SSH Key on Windows with Windows Subsystem for Linux

Add default SSH Keys

Connect to a GridPane server by SSH as Root user

When logged into your server, copy and paste the following command and hit enter (“domain.com” should be the domain you wish to optimize): –

gp -wp domain.com db optimize

#### Prevention

To prevent this from happening in the future, Redis object caching should help reduce this kind of behavior by a wide margin. Here is an overview of Redis object caching and how to use it on your website:

Using GridPane Redis Object Caching

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

