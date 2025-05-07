# Elasticsearch and ElasticPress | GridPane

# Elasticsearch and ElasticPress

 

7 min read 

## Introduction

Elasticsearch is a feature available to all our users on the developer plan. This is a great feature for anyone who has a site that has a lot of information, for example, a large news website or blog, a knowledgebase, or a large e-commerce store.

### Table of Contents

If you’re coming from a managed hosting provider, there’s a good chance you can save a lot of money by making the switch over to GridPane. You can run it on as many websites as you need, and there’s no per website fee attached.

One thing to note before you get started is that Elasticsearch can be resource-intensive.

 

## What is Elasticseach?

Elasticsearch is an open-source search engine. Its scope goes far beyond WordPress and can be used for things like analytics, spotting data trends, machine learning, and more.https://www.elastic.co/guide/en/elasticsearch/reference/current/elasticsearch-intro.html

For our purposes with WordPress, it’s an extremely fast and accurate search engine that replaces the default WordPress search function. You can use Elasticsearch and the ElasticPress plugin to index all of your website’s content, and then provide fast and accurate search results from this index faster than MySQL can run the same search.

You can use Elasticsearch to decrease search time, improve result accuracy, and create a customized search experience for your visitors.

The ElasticPress plugin has a great breakdown of all of the features it offers and it’s well worth a read:https://wordpress.org/plugins/elasticpress/

 

## Using Elasticsearch on GridPane

To get started with Elasticsearch, you first need to reach out to our support so we can install it for you on your server/s. We’ll have a toggle for this feature in the future, but for now please submit a support ticket with your server name and IP address and we’ll take care of it for you.

Once it’s been installed on your server you’ll then need to install and configure the ElasticPress plugin on your website/s.

 

 

### Information: DigitalOcean and Elasticsearch

In the past, Elasticsearch has had issues with servers on DigitalOcean, returning 451 errors during the installation process and causing it to fail. This no longer appears to be the case, but should it happen this is beyond our control and you may need to use a different provider.

## Configuring ElasticPress

### Step 1. Install the plugin

The plugin is available from the WordPress repo – simply search for ElasticPress, then install and activate it like any regular plugin.

### Step 2. Enter the Elasticsearch Host URL

Inside your settings page, we need to enter the host URL.

The Elasticpress.io tab is for their paid integration. We need the “Third Party/Self Hosted” tab, and then enter HTTP://localhost:9200 in the Elasticsearch Host URL box. Then click Save.

### Step 3. Index your content

Now we’ve connected the plugin to the server we can index your website’s content. You should automatically be taken to the page where you can begin the process. Depending on the size of your database this can take some time.

Once complete, you may wish to check the “Index Health” page, and hit the refresh button in the top right-hand corner.

### Step 4. Customize your search features

The ElasticPress plugin has a lot of customizable features that you can take advantage of to make your website’s search experience even better for your target audience.

Each section has a “learn more” dropdown with information about what each feature does.

The plugin also has two additional settings pages. One is for managing search fields and “weighting”. Weighting means prioritizing specific results, for example, giving weight to page titles or excerpts, etc when a user performs a search.

The other page is for creating custom search results.

Configure as needed 🙂

 

## ElasticPress Autosuggest

ElasticPress 2.4 introduced autosuggest, which is a very cool feature that will automatically make suggestions for your existing content when users begin typing in your search fields. Many of the world’s largest websites use this functionality.

### Using Autosuggest on GridPane

This is available on both Nginx and OpenLiteSpeed servers, but the setup and WordPress plugin settings are different for both.

To get started you’ll need to connect to your server – please see the following to get started:

 

Step 1. Generate your SSH Key

Step 2. Add your SSH Key to GridPane (also see Add default SSH Keys)

Step 3. Connect to your server by SSH as Root user (we like and use Termius)

 

## Enabling ElasticPress Autosuggest on Nginx

Inside Dashboard > ElasticPress > Features you’ll find the autosuggest feature.

Here you’ll see the following notice:

You aren’t using ElasticPress.io so we can’t be sure your host is properly secured. Autosuggest requires a publicly accessible endpoint, which can expose private content and allow data modification if improperly configured.

### Community Contribution

The following was provided to us by one of the GridPane community on how they implemented this on their website. You can also learn more here:

 

### Step 1. Create an Nginx Config

On your server, run the following command to create your ElasticPress auto-search config (switching out site.url for your URL):

```
nano /var/www/site.url/nginx/elasticautosearch-main-context.conf
```

This is the community code snippet, modified from the original snippet from 10up:

 

```
location /ep-autosuggest {
  # only allow POST requests
  limit_except POST {
    deny all;
  }

  # Perform our request
  rewrite ^/ep-autosuggest(.*) $1/_search break;
  proxy_set_header Host $host;

  # Use the URL of the server here
  proxy_pass http://localhost:9200;
  return 403;
}
```

Now save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

### Step 2. Check and Reload Nginx

Check the Nginx configuration file with:

```
nginx -t
```

If no errors are returned, reload Nginx with:

```
gp ngx reload
```

 

### Step 3. Enable Autosuggest Inside of WordPress

Back inside your website, add “ep-autosuggest” as your Endpoint URL, and set the status to Enabled.

Note the message that says “Enabling this feature will require re-indexing your content.“

When you’re ready, click Save.

 

## Enabling ElasticPress Autosuggest on OpenLiteSpeed (OLS)

Inside Dashboard > ElasticPress > Features you’ll find the autosuggest feature.

Here you’ll see the following notice:

You aren’t using ElasticPress.io so we can’t be sure your host is properly secured. Autosuggest requires a publicly accessible endpoint, which can expose private content and allow data modification if improperly configured.

Below we’ll look at how to safely configure this on OpenLiteSpeed.

 

### Step 1. Edit Your Website’s blocks.conf

On OpenLiteSpeed we’ve created the blocks.conf include where you can add custom rule blocks. The contents of this file are added directly to your website’s vhconf once it’s regenerated.

Edit this file with:

```
nano /var/www/site.url/ols/blocks.conf
```

Add the following to your file, but edit line 10 and replace siteurl with your URL, removing the period. For example, for GridPane.com this would be: context /gridpanecom-post-1/_search {.

 

```
extprocessor elastic {
  type                    proxy
  address                 localhost:9200
  maxConns                300
  initTimeout             60
  retryTimeout            60
  respBuffer              1
}

context /siteurl-post-1/_search {
  type                    proxy
  handler                 elastic
  addDefaultCharset       off
}
```

Now save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

### Step 2. Add a rewrite rule

Next, we need to add a rewrite rule. Rule the following command, replacing site.url with your URL:

```
nano /var/www/site.url/ols/rewrites.conf
```

Add the following, again replacing “siteurl” with your URL without the period:

```
RewriteRule /siteurl-post-1(.*) http://elastic/$1 [P]
```

For example:

```
RewriteRule /gridpanecom-post-1(.*) http://elastic/$1 [P]
```

Now save the file with CTRL+O followed by Enter. Exit nano with CTRL+X.

 

### Step 3. Regenerate Your Websites vhconf

Next, we need to regenerate your vhconf to add your updates with the following (replace site.url with your URL):

```
gpols site site.url
```

We’re now done with the server-side work.

 

### Step 4. Configure the plugin settings

In order for Autosuggest to work, the Endpoint URL box has to match the context path in step 1 but this time using the full URL, including the protocol:

https://site.url/siteurl-post-1/_search

Here I’ve used input[type=”search”] as the Autosuggest selector since it’s the core WordPress search box.

If for some reason it’s not working then it’s likely that you need to update the autosuggest selector.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

