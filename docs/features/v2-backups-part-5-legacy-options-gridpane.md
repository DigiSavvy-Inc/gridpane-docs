# V2 Backups Part 5. Legacy Options | GridPane

# V2 Backups Part 5. Legacy Options

 

1 min read 

### Table of Contents

 

## Introduction

On July 3rd 2024 we released a new ID format for backup buckets at AWS s3, Backblaze B2, and Wasabi. This change was introduced to ensure that you can easily re-add credentials to a website again if you disable them for any reason, or add new API credentials and continue using the same bucket.

This article details when you may need to use the legacy format in the future when attaching a remote storage option to your websites.

 

## When Should You Use the Legacy Format?

The legacy format can be used via a simple checkbox when configuring your remote backup options for a website. This should only be used in the following use cases:

 

## Backup Bucket UUID Formatting

For all remote backups that were configured before July 3rd 2024, these are now following the legacy backup Universally Unique Identifier (UUID) format:

```
gridpane-backups-${UUID}
```

In this case, configured specifically means adding a remote backup provider to a website, not simply modifying the purge options, or storage threshold settings, etc of an already configured website.

This has no effect on the backups taking place on these sites, and they will continue to work as normal.

### New UUID Format

For July 3rd 2024 onwards, each time you add a remote storage provider to a website, it will follow the new format:

```
gridpane-backups-${s3_secretkey:0:8}-${UUID}
```

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

