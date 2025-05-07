# Using ManageWP and ModSec | GridPane

# Using ManageWP and ModSec

 

3 min read 

Third-Party Software Notice
Our support team cannot provide support for third-party software and services. However, if you need assistance or spot an issue with this article please post in the [GridPane Community Forum](https://community.gridpane.com/), and we will make necessary updates/improvements where needed.

ModSecurity is a comprehensive and highly effective WAF, but out of the box it doesn’t always work with one of the more popular WordPress management services: ManageWP.

If you’re finding that ManageWP can’t connect to your site due to ModSec, this article will walk you through how to set up a server-wide exception rule that will allow these to both work together on all of the websites on your server.

 

## Step 1: Check the Nginx Error Log and Find the Error ID

In our testing the error ID has consistently been 949110, but you may want to quickly confirm.

### Locate the Error ID

To find the error ID, we need to check the Nginx Error Site Log. This article assumes that you’ve already encountered an error using ManageWP and ModSec together.

Open up your websites configuration modal inside your GridPane account, and then click through to the logs tab and open up the Nginx Site Error Log:

We’re looking for the following to identify the request that ModSec has blocked:

```
[file "/etc/nginx/modsec/owasp/rules/REQUEST-912-DOS-PROTECTION.conf"]
```

In it’s entirety, the error will look like this:

```
2020/05/16 16:28:53 [error] 13237#13237: *3665 [client 127.0.0.1] ModSecurity: Access denied with code 403 (phase 2). Matched "Operator `Ge' with parameter `10' against variable `TX:ANOMALY_SCORE' (Value: `52' ) [file "/etc/nginx/modsec/owasp/rules/REQUEST-949-BLOCKING-EVALUATION.conf"] [line "80"] [id "949110"] [rev ""] [msg "Inbound Anomaly Score Exceeded (Total Score: 52)"] [data ""] [severity "2"] [ver ""] [maturity "0"] [accuracy "0"] [tag "application-multi"] [tag "language-multi"] [tag "platform-multi"] [tag "attack-generic"] [hostname "127.0.0.1"] [uri "/wp-load.php"] [unique_id "158964653354.518729"] [ref ""], client: 127.0.0.1, server: waas.monster, request: "POST /wp-load.php?mwprid=5ec014c4edf430.71392005 HTTP/1.1", host: "yourwebsite.com", referrer: "https://yourwebsite.com/"'
```

You should be able to quickly narrow down your search with the timestamp – although note that your server is likely set to UTC time as default.

Once you’ve found your error, you need to note down the ID as we’ll be using this for our exclusion rule.

In our testing above you can see that the ID is indeed the one we were expecting to find:[id “949110“]

 

 

### UPDATE

The recent update to ModSecurity now requires a backslash at the end of each line except for the last one. Examples are included in the file itself, and we have updated the snippet below so it's now up-to-date.

## Step 2: Create our ManageWP Exception

First we need to open up the configuration file where we’ll add our exclusion. To do this, run the following command:

```
nano /etc/nginx/modsec/owasp/rules/REQUEST-900-EXCLUSION-RULES-BEFORE-CRS.conf
```

The code below contains all of the ManageWP IP addresses as per the ManageWP whitelisting page. At the very end you’ll see the “ctl:ruleRemoveById=949110”. If by chance your ID was different to the one we were expecting, replace the 949110 with the error ID you located above in step 1.

Now add your code to the very end of the file (use your arrow keys to navigate).

```
SecRule REQUEST_HEADERS:X-Real-IP "@ipMatch 34.211.180.66,54.70.65.107,34.210.224.7,52.41.5.108,52.35.72.129,54.191.137.17,35.162.254.253,52.11.12.231,52.11.29.70,52.11.54.161,52.24.142.159,52.25.191.255,52.34.126.117,52.34.254.47,52.35.82.99,52.36.28.80,52.39.177.152,52.41.237.12,52.43.13.71,52.43.76.224,52.88.96.110,52.89.155.51,54.187.92.57,54.191.32.65,54.191.67.23,54.191.80.119,54.191.135.209,54.191.136.176,54.191.148.85,54.191.149.8,52.26.122.21,52.24.187.29,52.89.85.107,54.186.128.167,54.191.40.136,52.88.119.122,52.89.94.121,52.25.116.116,52.88.215.225,54.186.143.184,52.88.197.180,52.27.171.126,34.211.178.241,52.24.232.158,52.26.187.210,52.42.189.119,54.186.244.128,54.71.54.102,34.210.35.214,34.213.77.188,34.218.121.176,52.10.190.191,52.10.225.96,52.11.187.168,52.25.139.76,52.43.127.200,54.191.108.9,54.70.201.228,44.224.174.169,52.32.57.81,44.225.177.160,34.223.186.249,44.224.135.238,44.226.111.14,44.225.203.104,44.226.100.122,44.224.250.144,44.225.118.211"\
"id:3,\
phase:1,\
nolog,\
allow,\
pass,\
ctl:ruleRemoveById=949110"
```

Writing to and saving a file in nano is a three-step process:

Next we need to test and reload the Nginx config.

Test the config with the following command – if there are any errors do NOT continue and reload Nginx.

```
nginx -t
```

If no errors are present then reload Nginx with this command:

```
gp ngx reload
```

You’ve now set up your exclusion rule for ManageWP inside ModSec and you can now use the service with all of the websites on your server.

For more detailed information about using ModSec, please checkout:

Site Firewalls: ModSecurity

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

