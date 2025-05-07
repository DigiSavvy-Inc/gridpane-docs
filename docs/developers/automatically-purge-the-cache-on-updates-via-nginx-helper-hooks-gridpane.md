# Automatically Purge the Cache on Updates via Nginx Helper Hooks | GridPane

# Automatically Purge the Cache on Updates via Nginx Helper Hooks

 

2 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

The code in this article was contributed by a GridPane client and made public over in the GridPane Community Forum in this thread:

https://community.gridpane.com/t/gridpane-cache-and-plugin-updates/644/5

It’s not something that we can provide support for, however, we have tested it and found that it all works as expected, as have many other GridPane clients. You can also sign up for the community here and ask any questions you may have in the above thread.

### Adding the code to your website

You can add this snippet to your site in a few different ways:

If you’re interested in the custom plugin route, Sridhar Katakam has a free starter plugin you could use here:

https://github.com/srikat/my-custom-functionality

### The code

 

```
//* Nginx Helper Enhancement
function nhpcau_upgrader_process_complete() {

  global $nginx_purger;

  if(isset($nginx_purger))
  {
    $nginx_purger->purge_all();
  }
}
// After plugins have been updated
add_action( 'upgrader_process_complete', 'nhpcau_upgrader_process_complete', 10, 0 );

// After a plugin has been activated
add_action( 'activated_plugin', 'nhpcau_upgrader_process_complete', 10, 0);

// After a plugin has been deactivated
add_action( 'deactivated_plugin', 'nhpcau_upgrader_process_complete', 10, 0);

// After a theme has been changed
add_action( 'switch_theme', 'nhpcau_upgrader_process_complete', 10, 0);
```

Once active, this will automatically purge the cache when:

## Verify it’s working

To verify that the code is working as expected, you can do the above actions while checking the website’s response headers for a HIT and MISS response. To learn how to do this, please see the first part of our Diagnosing Caching Issues article:

Diagnosing Caching Issues

Or, alternatively, check out (and bookmark) this website by Hubert Nguyen (who’s also a member of the GridPane community):

https://test.ismypagecached.com/

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

