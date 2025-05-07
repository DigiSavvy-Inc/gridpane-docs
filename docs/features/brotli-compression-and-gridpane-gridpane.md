# Brotli Compression and GridPane | GridPane

# Brotli Compression and GridPane

 

2 min read 

Brotli is a compression algorithm developed by Google, and is supported by all major web browsers as of 2019.

By default, Brotli is not enabled on GridPane servers, however, we have the following GP-CLI commands that will allow you easily enable or disable Brotli on a per website basis:

 

```
gp site {site.url} -brotli-on
```



Enabling will set Brotli as the default compression method. To disable Brotli and renable Gzip use:

```
gp site {site.url} -brotli-off
```

 

## Why isn’t Brotli Enabled by Default?

We don’t have Brotli enabled on GridPane by default as it can require fine-tuning to make it more performant than Gzip on dynamic websites (like those that run on WordPress).

Brotli technically does have the edge when it comes to compressing files, meaning that it can make them smaller than Gzip is able to. However, it also takes longer to process, which out-of-the-box may result in slower load times.

The data from available test write-ups over the past 5 years suggest that:

It all depends of course, but it makes very little real-world difference to page speed unless users take advantage of the Brotli Static directive and make sure that all assets are pre-compressed with Brotli in the build process.

Doing this can make a great difference, but there’s likely not going to be a justifiable benefit to using Brotli without first pre-compressing.

 

## Configuring Brotli

You’re almost certainly using an SSL, but if not, HTTPS is a requirement for Brotli to work so you will need to provision an SSL on any website you wish to use it on.

Once enabled, the following settings are the defaults:

```
brotli on;brotli_static on;brotli_comp_level 4;brotli_types application/atom+xml    application/javascript    application/json    application/ld+json    application/manifest+json    application/vnd.geo+json    application/vnd.ms-fontobject    application/x-font-opentype    application/x-font-truetype    application/x-font-ttf    application/x-javascript    application/x-web-app-manifest+json    application/xhtml+xml    application/xml    application/xml+rss    image/bmp    font/eot    font/opentype    font/otf    image/svg+xml    image/vnd.microsoft.icon    image/x-win-bitmap    image/x-icon    text/cache-manifest    text/css    text/javascript    text/plain    text/vcard    text/vnd.rim.location.xloc    text/vtt    text/x-component    text/x-cross-domain-policy    text/xml;
```

Note: brotli_static on; only looks for pre-compressed files to serve. It doesn’t pre-compress them.

You can view these settings directly inside the brotli.conf with:

```
cat /etc/nginx/common/brotli.conf
```

If you want to adjust the types or the compression level, then make a copy of this file and store it in /etc/nginx/common/_custom/brotli.conf and then your custom settings will persist.

You can do this with the following command:

```
cp /etc/nginx/common/brotli.conf /etc/nginx/common/_custom/brotli.conf
```

Edit your _custom/brotli.conf with:

```
nano /etc/nginx/common/_custom/brotli.conf
```

And then save the file with CTRL+O and then Enter. Exit nano with CTRL+X.

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

