# How to Fix the PHPMyAdmin “Bad Userdata” Error | GridPane

# How to Fix the PHPMyAdmin “Bad Userdata” Error

 

1 min read 

Opening PHPMyAdmin (PHPMA) for both your live websites and staging sites is usually very quick and easy – you simply click on the little database icon next to your site, and PHPMA will open up in a new window and instantly log you in.

If you’re experiencing a “Bad Userdata” error when you open up PHPMA, this means that your database credentials do match up with the credentials that are stored in the Gridpane Panel.

Fortunately, this kind of issue is extremely rare and also very easy to fix.

### Step 1. First Connect to Your Server via SSH

If this is your first time, please see the following articles to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

### Step 2. Run Our GP-CLI to Fix the Mismatch

Now on the command line, simply copy and paste the following command, switching out site.url for your actual website URL:

```
gp site site.url -dbcreds
```

For example:

```
gp site example.com -dbcreds
```

The above command will update the credentials stored in GridPane Panel to match the ones in the server, and you will now be able to access your PHPMA again.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

