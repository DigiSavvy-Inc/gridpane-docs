# How to extract a subsite from a multisite and set it up as a regular WordPress install with AIO | GridPane

# How to extract a subsite from a multisite and set it up as a regular WordPress install with AIO

 

2 min read 

All in One WP Migration (AIO) is an excellent plugin for moving a WordPress website from one place to another, and also for extracting a subsite from a WordPress multisite installation.

In this article, we’ll look at how to extract a subsite and then recreate it on its own WordPress install – completely standalone and multisite free.

This can be handy when a subsite is growing too large in size, or is too database-intensive and is creating issues for other sites in the network.

## Part 1. Extracting your subsite

Inside your multisite, install and activate the All in One WP Migration plugin and Multisite extension, and then click through to the export option inside AIO. Select the subsite you wish to extract and click the “Export to” button and choose your preferred method.

## Part 2. Importing your subsite into a fresh WordPress installation

First create your website, and install the All in One WP Migration plugin – the multisite extension isn’t needed to import your website.

### Method 1 – The irregular, but proven way

Now, in our testing, importing the regular way hasn’t worked. The workaround for this is to upload your file via SFTP and then run your import from there.

To connect to your server via SFTP please check out either one of these two articles:

Connect to a GridPane Server by SFTP as the Root User

Connect to a GridPane Server by SFTP as a System User

Once inside your server navigate through into:

www > yourdomain.com > htdocs > wp-content > ai1wm-backups

```
/var/www/yourdomain.com/htdocs/wp-content/ai1wm-backups
```

And upload your website inside this folder.

Once the upload is complete, head back inside your new WordPress site, and click through to/wp-admin/admin.php?page=ai1wm_backups

Click restore to import your site:

This failing the regular way may be a temporary quirk in the plugin, but the SFTP upload has been 100% reliable for us.

Method 2 – The regular, but unproven way

Before you begin, we recommend you create a manual backup on your new install as if you upload the regular way and it fails, it will likely wreck your website and this will save you from having to rebuild it again by simply restoring the backup.

Upload your multisite the same way you would any regular website with the AIO plugin. Head to the AIO import page inside your site:/wp-admin/admin.php?page=ai1wm_import

Upload your file, and follow the prompts to run the import. It will give you a notification once the import has completed.

## Part 3. Login, confirm everything’s working correctly, and set up new users if required.

To set up new admin credentials simply click the Single Sign On (SSO) button to login in and head to/wp-admin/users.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

