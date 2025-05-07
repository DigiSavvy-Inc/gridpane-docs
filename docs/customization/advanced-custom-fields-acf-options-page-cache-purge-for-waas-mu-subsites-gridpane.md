# Advanced Custom Fields (ACF) Options Page Cache Purge for WaaS/MU Subsites | GridPane

# Advanced Custom Fields (ACF) Options Page Cache Purge for WaaS/MU Subsites

 

1 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

The following is another solution from one of our users, shared with the community in the Facebook Group. It will help clear the cache on the ACF options page on WaaS network / multisite installation subsites when changes are made.

You can learn more about the ACF options page here:https://www.advancedcustomfields.com/resources/options-page/

Important: This is not our code and it is not supported by GridPane. The responsibility falls on you for its correct testing, implementation, and upkeep.

The custom function:

```
function clear_nginx_helper_cache() {do_action('rt_nginx_helper_purge_all');}add_action('acf/save_post', 'clear_nginx_helper_cache', 20);
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

