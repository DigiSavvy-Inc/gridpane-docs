# Remote Backups: Create and Set Your AWS S3 API Credentials | GridPane

# Remote Backups: Create and Set Your AWS S3 API Credentials

 

3 min read 

### Table of Contents

 

## Introduction

Amazon Simple Storage Service (Amazon S3) is Amazon’s object storage service. It’s cheap and secure, and an excellent option for remote backups. This article will walk you through how to generate your S3 API keys and add them to your GridPane account.

 

 

### Information

Currently, the IAM user requires all access. We're looking into restricted access and we will update this article as the new backup system develops further.

## Step 1. Sign in to the IAM console

Log in to your IAM console.

Once inside the console, choose Policies in the left navigation pane.

![IAM_Management_Console_-Policy_Screen_.png](https://s3.us-east-2.wasabisys.com/gridpanekb/Provisionn-Amazon-Lightsail-server-using-the-AWS-Lightsail-API/IAM_Management_Console_-Policy_Screen_.png) 

## Step 2. Create an Amazon S3 GridPane policy

In the Policies, panel click the blue Create policy at the top of the page.

On the following page you’ll need to add the “S3” service into the search bar and select it as the service you wish to create a policy for.

Then check the “All S3 Actions” checkbox.

Next click on resources and select All resources.

You can then click the Review policy button at the bottom of the page.

Next give your policy a name and a description and click the Create policy button. You’ll need to remember your policy name for the next step.

 

## Step 3. Create a Key and Secret

Next, still in the IAM console, choose users from the left-hand navigation and then click on Add User on the following page.

### Part 1

Here you need to give your new user a name and check the programmatic access checkbox.

### Part 2

Select “Attach Existing Policy Option” and then search for the name of the policy you created in step 2.

### Part 3

This is optional, feel free to skip it and click the “Next: Review” button.

### Part 4

Here you can review your information, confirm it’s correct, and then click the Create User button.

### Page 5

This next page contains your new Access Key ID and Secret access key for your user. These will NEVER be shown again so it’s important you note them down, or alternatively you can download these credentials as a CSV file.

Your credentials have now been created. Now it’s time to add them to your GridPane account.

 

## Step 4. Add your Amazon S3 API credentials to GridPane

Back in your GridPane account, click through to your settings page:

Here, click through to the Integrations page, click Backup Providers, and enter your API details in the AWS S3 tab:

Give your key a name, enter your details API details, select your provider from the dropdown, and then click the Create button.

You’re all set! To learn how to configure remote backups for your websites check out the following article for a full walk-through:

Remote Website Backups

 

## Further Reading

For further information about how backup systems work, the available options for configuring them, and for setting up remote backups (available on V2), please see the articles listed below.

### Strategy

Recommended Backup Strategy

### V2 Backup Documentation

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

