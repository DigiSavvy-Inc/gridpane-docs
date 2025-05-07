# WP Feedback and Cache Purging | GridPane

# WP Feedback and Cache Purging

 

2 min read
We recently had a user who solved a caching issue with the WP Feedback plugin and was kind enough to share that code with us, so that we could share it with the GridPane community.

They’ve also shared the post with the WP Feedback team who were very responsive and are making plans to integrate cache clearing into their plugin.

All of which is awesome 🙂

Below is a description of the problem followed by the solution.

Important: This is not our code and it is not supported by GridPane. The responsibility falls on you for its correct testing, implementation, and upkeep.

## The Problem

When a comment was posted to a task inside the WP Feedback task center here:

website.com/wp-admin/admin.php?page=wpfeedback_page_tasks

The new comment could take a significant amount of time to appear, instead of being posted immediately.

## The Solution

There are actually two solutions that we’ll cover, both from the same GP user.

### Method 1

The first is as follows:

```
function relywp_clear_cache() {        if(strpos($_SERVER['REQUEST_URI'], 'admin.php?page=wpfeedback_page_tasks') !== false){                wp_cache_flush();                opcache_reset();        }}add_action( 'admin_head', 'relywp_clear_cache' );
```

This will clear the cache when the page is loaded.

### Method 2

This second method will clear the cache only when a comment is made.

It’s important to note that this overwrites the “wpf_crm_new_comment” function from the plugin via the action hook and adds 2 lines to clear the cache at the end. So, while this is a more efficient cache clearing method, it means that if the “wpf_crm_new_comment” function ever gets updated in a new version, it will still be running the old version of the function since it’s being overwritten. Here’s the code:

```
add_action("init", function() { remove_action('wpf_crm_new_comment_action','wpf_crm_new_comment');});add_action("wpf_crm_new_comment_action", function() { $url = WPF_CRM_API.'wp-api/comment/store'; $new_comment = get_comment($comment_id); if($new_comment->comment_date_gmt=='0000-00-00 00:00:00'){ $new_comment->comment_date_gmt = get_gmt_from_date($new_comment->comment_date); } $new_comment->comment_type = wpf_api_func_get_comment_type($new_comment); $new_comment->task_id = $new_comment->comment_post_ID; $new_comment->wpf_site_id = get_option('wpf_site_id'); $response = json_encode($new_comment); wpf_send_remote_post($url,$response);  wp_cache_flush(); opcache_reset();});
```

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

