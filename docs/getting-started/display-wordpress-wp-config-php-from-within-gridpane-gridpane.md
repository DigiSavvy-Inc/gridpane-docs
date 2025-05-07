# Display WordPress wp-config.php from within GridPane. | GridPane

# Display WordPress wp-config.php from within GridPane.

 

1 min read 

To quickly view the contents of any of your GridPane site’s wp-config.php file follow the following steps.

## Step 1.  Go to the Sites Section of the GridPane Control Panel

Click on the sites link in the GridPane main menu to see all your active GridPane WordPress sites.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2259'%20height='114'%20viewBox='0%200%202259%20114'%3E%3C/svg%3E)## Step 2. Open the Site Customization Panel for your Active site

In the Active Sites panel, click on the domain in the URL column to open the Site Customization modal for the site whose WordPress configurations you wish to view.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2336'%20height='498'%20viewBox='0%200%202336%20498'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Display-WordPress-wp-config-php-from-within-GridPane/5d77be20a5168.png)## Step 3. Display your chosen site’s WordPress Configurations

From the Site Customizer you can display the contents of a site’s wp-config.php file by clicking on the Display wp-config icon link.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='1059'%20height='569'%20viewBox='0%200%201059%20569'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Display-WordPress-wp-config-php-from-within-GridPane/5d77be21aa3ee.png)A popup modal will appear containing the contents of your chosen site’s wp-config.php file.

![](data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20width='2111'%20height='4122'%20viewBox='0%200%202111%204122'%3E%3C/svg%3E)![](https://s3.us-east-2.wasabisys.com/gridpanekb/Display-WordPress-wp-config-php-from-within-GridPane/5d77be22eae2b.png)## GridPane wp-config.php location

GridPane servers store a site’s wp-config.php file in a secure non-web-accessible location above the core files directory. While this location is not the default location, it is completely normal as WordPress looks in both the core root directory and the parent directory for the wp-config file. This can be confirmed by checking WordPress core here.

If you wish the view the wp-config.php via SFTP you will find it here:

```
/var/www/{site.url}/wp-config.php
```

(SFTP as root)

```
/sites/{site.url}/wp-config.php
```

(SFTP as system-user)

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

