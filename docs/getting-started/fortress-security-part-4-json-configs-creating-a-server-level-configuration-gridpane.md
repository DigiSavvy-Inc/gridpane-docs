# Fortress Security Part 4. JSON Configs & Creating a Server-Level Configuration | GridPane

# Fortress Security Part 4. JSON Configs & Creating a Server-Level Configuration

 

4 min read 

### Table of Contents

 

 

### Fortress schema.json

For those of you that use PhpStorm or Visual Studio Code for development, Fortress offers a complete JSON schema for its config that you can use in your editor for auto-complete and validation.

You can download/reference it here.

## Introduction

Fortress can be configured via WP-CLI and editing its JSON configuration where the majority of its settings are stored. Before you begin, please ensure you have read through our part 2 article, where we cover each of the Fortress modules in more detail.

This article will walk you through working directly with the following files:

We typically recommend configuring the website level config.json via WP-CLI and we’ll primarily focus on editing the server-config.json in the sections below.

 

## JSON Configuration File Order

We covered this in detail in Part 2 of this series, but for quick reference, here is the rundown again. Fortress has 3 JSON files which determines what settings are active on each different module. These are:

###### Baseline (default) configuration

The baseline configuration is what Fortress ships out of the box. To view the most up-to-date Fortress baseline configuration, please check the official developer documentation linked below. Fortress Baseline Configuration

###### Server level configuration

The server-config.json can be used to customize your own settings and apply them to ALL websites on a server. These settings override the baseline configuration.

###### Website level configuration

The config.json is the site-level config file. It can be configured on a per-site basis, and any settings here will override the baseline and server-config.json files.

 

## Editing Fortress JSON Configs

If you would like to customize the default Fortress configuration for ALL websites on a server we recommend that you first create and test the settings you want to set live on an individual test website.

While Fortress does include a --source=server flag in its CLI, this can’t be used on GridPane as the server-config.json cannot be edited by a website system user.

However, you can run the regular WP-CLI to create your desired configuration, test it, and then copy it from your website config.json flag to the server-config.json.

Configs are located as follows on GridPane servers:

```
/etc/fortress/server-config.json
```

```
/var/www/site.url/fortress/config.json
```

The complete configuration reference can be found here.

 

 

### Important

Before you set any config changes live on a production website (or all production websites via the server config), please ensure you have thoroughly tested before settings your changes live. This can be done on a staging site, a clone, or a website that create solely for testing.

## Editing the Site Configuration File

You can create and edit the site specific config.json file with the following command (replace site.url with your website URL):

```
nano /var/www/site.url/fortress/config.json
```

For example:

```
nano /var/www/mywebsite.com/fortress/config.json
```

Once you’ve added your customizations, save the file with CTRL+O, followed by Enter. Now you can exit nano with CTRL+X.

### Fortress Syntax Check

To ensure that your configuration is valid, Fortress has its own syntax check that you can run with this WP-CLI command (replace site.url with your website URL):

```
gpfort site.url -cli fort config test --reload-on-success
```

This will automatically clear the Fortress cache if successful. If unsuccessful, Fortress will provide you with detailed troubleshooting information.

Once you’ve tested your config, you can now copy its contents and add it to your server-config.json to apply to all websites on a server.

 

## Editing the Server Configuration File

First, you need to create the following directory to store your config:

```
mkdir /etc/fortress
```

You can now both create and edit the server-level configuration file with the following command:

```
nano /etc/fortress/server-config.json
```

Once you’ve added your customizations, save the file with CTRL+O, followed by Enter. Now you can exit nano with CTRL+X.

### Fortress Syntax Check & Reload

To ensure that your configuration is valid, Fortress has its own syntax check that you can run with this WP-CLI command. This check can be ran via the following command:

```
gpfort all-sites -cli fort config test --reload-on-success
```

This is similar to the nginx -t syntax check and will automatically clear the Fortress cache if successful. If unsuccessful, Fortress will provide you with detailed troubleshooting information.

The above command will reload each website configuration one by one.

 

## Example Pillars Configuration

Below is an example of our recommended default Pillars for WordPress Core settings/option:

 

```
{
  "vaults_and_pillars": {
    "option_pillars": {
      "users_can_register": {
        "value": "0"
      },
      "blog_public": {
        "value": "1"
      },
      "permalink_structure": {
        "value": "/%postname%"
      },
      "tag_base": {
        "value": ""
      },
      "category_base": {
        "value": ""
      },
      "default_role": {
        "value": "subscriber"
      }
    }
  }
}
```

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

