# What Does “FastCGI sent in stderr” Mean Inside Nginx Website Error Logs? | GridPane

# What Does “FastCGI sent in stderr” Mean Inside Nginx Website Error Logs?

 

3 min read 

### Table of Contents

 

## Introduction

A common point of confusion when examining Nginx website error logs is why “FastCGI” appears there, even when FastCGI caching isn’t enabled on that particular website.

In this article, we’ll take a look at what “FastCGI” actually is, an example of this kind of error, and where these errors stem from.

 

## What is “FastCGI”?

Before FastCGI there was CGI, which stands for “Common Gateway Interface.” This is a protocol for a web server to pass a website visitor’s request to a server-side application and then receive the requested data back to send to the visitor.

FastCGI is the evolved, more efficient, and feature-rich update that solves the performance problems inherent in the original CGI protocol. This Technical Whitepaper digs deeper into the topic.

 

## FastCGI and PHP-FPM

PHP-FPM stands for PHP FastCGI Process Manager. It’s a FastCGI daemon for PHP, which allows it to run as an isolated service, as well as offering numerous other advantages for high-traffic WordPress websites and other PHP applications.

When deployed with Nginx, the Nginx web server processes HTTP/HTTPS requests, and hands off the rest of the work. When server page caching is enabled, any already cached pages will be returned to the requestor without the need for PHP processing. When a cached version of the request is not available, PHP-FPM will process any PHP code necessary to complete the request.

### Not to be confused with FastCGI Page Caching

The FastCGI caching mechanism is an Nginx module that uses the FastCGI protocol. Because of this, it’s commonly referred to as “FastCGI caching”, however, this is a separate mechanism from PHP-FPM.

 

## What Does “FastCGI sent in stderr” Mean Inside Nginx Website Error Logs?

Here’s a recent example of a question we received:

 

A few months ago, I switched from FastCGI page caching to Redis Page Caching. I updated my settings in the NGINX helper plugin to reflect the change. But now, my NGINX error logs have multiple references to FastCGI errors.

 

Here’s an example of the error in question:

```
2022/11/17 07:04:10 [error] 29582#29582: *10257 FastCGI sent in stderr: "PHP message: get_cart was called incorrectly. Get cart should not be called before the wp_loaded action. Backtrace: require('wp-blog-header.php'), require_once('wp-load.php'), require_once('/var/www/example.com/wp-config.php'), require_once('wp-settings.php'), do_action('init'), WP_Hook->do_action, WP_Hook->apply_filters, WFACP_OXY->init_extension, WFACP_OXY->editor_prepare_module, WFACP_Template_loader->load_template, do_action('wfacp_template_load'), WP_Hook->do_action, WP_Hook->apply_filters, WFACP_Compatibility_With_WC_Points_and_Reward->actions, WC_Points_Rewards_Cart_Checkout->render_earn_points_message, WC_Points_Rewards_Cart_Checkout->get_points_earned_for_purchase, WC_Cart->get_cart, wc_doing_it_wrong. This message was added in version 2.3.PHP message: get_cart was called incorrectly....
```

This is a common question, simply because the name “FastCGI caching” can be confusing if you don’t have context in the previous sections above.

### FCGI_STDERR

The FCGI_STDERR packet type is used to send standard error information from the application to the web server. It is then logged inside your website’s Nginx error log.

In a nutshell, this means these errors are coming directly from your application (WordPress), and it’s your website itself that’s generating these errors and requires troubleshooting.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

