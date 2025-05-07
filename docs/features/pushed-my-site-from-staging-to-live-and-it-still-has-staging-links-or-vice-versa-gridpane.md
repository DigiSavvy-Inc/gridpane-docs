# Pushed my site from staging to live and it still has staging links or vice versa. | GridPane

# Pushed my site from staging to live and it still has staging links or vice versa.

 

1 min read 

 

### End of 2020 Update

We have dramatically improved our cloning/staging push processes, and this update included replacing WP-CLI Search Replace with Interconnectit Search Replace. This is a far more reliable tool, even more so than most plugins.

When you push from staging to live or live to staging, we automatically do find and replaces of URLs in the database. We don’t change emails, or other items, just URLs. Sometimes our find and replace is unable to replace all of the URLS.

When that happens, you may need to use an extra plugin. Users have had good results out of the following plugins:

Velvet Blues – https://wordpress.org/plugins/velvet-blues-update-urls/ it’s old, but seems to still work very well.

Go Live Update URLs – https://wordpress.org/plugins/go-live-update-urls/

Once you run this, do a full cache clear via our Tools > Quick Fix > Clear All Nginx Caches.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

