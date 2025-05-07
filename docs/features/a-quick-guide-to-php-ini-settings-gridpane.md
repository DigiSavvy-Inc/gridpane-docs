# A Quick Guide to PHP INI Settings | GridPane

# A Quick Guide to PHP INI Settings

 

6 min read 

### Table of Contents

 

 

### Information

This is a supplementary article to our Configure PHP guide.

## Introduction

PHP INI settings are configuration directives that control how PHP executes scripts, manages resources, handles errors, and processes requests on the server. These settings impact performance, security, and functionality for your WordPress websites, and while our default settings are fine for 99% of websites, this article covers when you may need to make adjustments to these settings.

Unlike many hosts, GridPane allows you to configure these settings on a per-site basis. In this article, we’ll cover how these settings apply to WordPress websites as individual applications.

### Changing Your PHP INI Settings

To update your PHP INI settings, we highly recommend that you use the new tab inside your GridPane account dashboard.

You can open up your site customizer by clicking the site’s domain name inside the Sites page of your GridPane account.

PHP settings are inside the PHP tab. Before you can make changes, you may need to sync your settings. You can do this by clicking the Sync PHP Settings button:

 

## 1. Max Execution Time (seconds)

#### GridPane default: 300 seconds (5 minutes)

This setting controls how long a PHP script can run before it’s stopped. WordPress uses PHP scripts for tasks like importing content, running updates, and processing large operations.

#### Need to know:

### Performance Implications

A high Max Execution Time can result in long-executing PHP scripts hogging CPU and resources, potentially leading to an equivalent of a Denial of Service (DoS) attack. In some cases, an attacker might even be able to exploit long-running scripts to shut down your website effectively.

#### Examples:

#### Protecting Against Performance Issues:

 

## 2. Max File Uploads

#### GridPane default: 20

This setting limits the number of files that can be uploaded in a single request. If you upload multiple images, PDFs, or media files at once, this setting controls how many can be processed at the same time.

This setting also affects WooCommerce product imports and some form plugins that allow multiple file uploads.

#### Need to know:

 

## 3. Max Input Time (seconds)

#### GridPane default: 60 seconds

This setting defines how long a script can take to receive input (such as form submissions, file uploads, and saved posts/pages) before timing out.

#### Need to know:

 

## 4. Max Input Vars

#### GridPane default: 5000

This setting limits the number of input variables (GET/POST requests). WordPress themes and plugins, especially ones with complex settings, can generate a lot of input fields.

#### Need to know:

 

## 5. Memory Limit (MB)

#### GridPane default: 256 MB

This setting defines the amount of memory PHP scripts can use. More memory is needed to run large plugins, handle many users, and process heavy scripts.

#### Need to know:

 

## 6. Post Max Size (MB)

#### GridPane default: 512MB

This sets the maximum size of a POST request. This affects file uploads and form submissions.

#### Need to know:

 

## 7. Default Socket Timeout (seconds)

#### GridPane default: 60 seconds

This setting defines how long PHP waits for data when communicating with external sources (APIs, external websites, payment gateways, etc).

#### Need to know:

 

## 8. Session Cookie Lifetime (seconds)

#### GridPane default: 0 seconds

This setting controls how long a session cookie remains active before expiring. A setting of 0 means it lasts until the browser is closed.

#### Need to know:

 

## 9. Session GC Maxlifetime (seconds)

#### GridPane default: 1440 (24 minutes)

This setting determines how long PHP keeps session data before it is deleted (garbage collected). Sessions store temporary data, such as user login states, shopping cart contents, and form entries.

WordPress does not rely heavily on PHP sessions, as it primarily uses cookies for user authentication. However, some plugins – particularly those related to e-commerce, memberships, and user management – may use PHP sessions.

#### Need to know:

 

## 10. Short Open Tag (On/Off)

#### GridPane default: Off

Turning this setting ON allows the use of (<? instead of <?php) in PHP files.

#### Need to know:

### Why would your site need this Setting turned ON?

A WordPress site would only require PHP short open tags to be ON if the site breaks with it off. Here are the most common reasons:

 

## 11. Upload Max Filesize (MB)

#### GridPane default: 512MB

This setting controls the maximum file size you can upload via the WordPress media library.

#### Need to know:

 

## Further Reading

To learn more about server-level PHP settings, PHP workers, and how to configure your PHP settings, please check out these articles:

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

