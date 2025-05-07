# PCI Compliance & GridPane | GridPane

# PCI Compliance & GridPane

 

6 min read 

 

### Important

The information provided in this knowledge base article is to provide a starting point for understanding your PCI compliance requirements, but it is not legal advice, or specific to your individual circumstances and legal obligations. PCI compliance extends beyond your website hosting environment, and it is the responsibility of the business owner to understand the requirements for accepting online payments.

### Table of Contents

 

## Introduction

PCI compliance stands for “Payment Card Industry” compliance. It’s a set of rules and standards designed to keep credit card information safe and secure when people make purchases both online and in person.

If a business wants to accept credit card payments, it needs to follow and meet the criteria laid out by the PCI Security Standards Council. Learn more directly on their website here:

PCI Security Standards Overview

 

## Does GridPane Offer PCI Compliant Hosting?

GridPane does not process, transmit, or store cardholder data on our platform. We also don’t operate your website on any of our plans (including fully managed), and we do not interact with your end users.

It is certainly possible to be PCI compliant on our platform, but we cannot guarantee PCI compliance, and we also cannot audit your site to verify that your business is compliant. This is beyond the scope of our services and ultimately beyond our control.

 

## Simplifying PCI Compliance: Third-Party Payment Processors

The most straightforward road to meet your PCI DSS requirements is to use a third-party payment process such as Stripe or PayPal, whose services are already PCI compliant.

Stripe, PayPal, and other compliant processors securely manage credit card processing for you, reducing the risk and complexity involved in achieving PCI compliance and negating the need for your business to store this sensitive information itself.

As they are already compliant, the bulk of the heavy lifting in terms of security and compliance, including the most complex aspects, is already done.

Important: While third-party payment processors may handle the bulk of PCI compliance, your business is still responsible for ensuring the integration is secure and that you’re following the correct PCI guidelines for your specific situation.

 

## WordPress Third-Party Payment Processor Integrations

The WordPress ecosystem offers a wide range of solutions to integrate your website with third-party payment processors. These solutions usually offer their own advice and guidelines on PCI compliance. Below are links from some of the more popular solutions, but a simple Google search will usually help you find the information you need.

 

## PCI Scan Compliance

When using a third-party payment processor like Stripe or PayPal, quarterly PCI scans might not be necessary, but this depends on how your business interacts with cardholder data.

### Minimal Handling of Card Data

If you use Stripe, PayPal, or a similar service, and your business does not store, process, or transmit any credit card data directly (because the payment processor handles all of that), you generally fall under a simpler PCI compliance category, like SAQ A. In this case, quarterly PCI scans are typically not required.

### Embedded or Hosted Forms

If you’re using a simple integration, such as a hosted payment page (where customers are redirected to Stripe or PayPal’s website to complete their transaction) or embedding their payment form on your site, the processor handles all sensitive data. This usually means you’re not required to perform quarterly scans.

Embedded and/or hosted forms can be the most optimal solution where possible, as they are designed to meet PCI compliance and reduce your exposure to sensitive data.

 

## Best Practices for PCI Compliance

Even when using a third-party payment processor, there are still important best security practices to follow to ensure that your online payments are secure and your business remains compliant. Here are some key practices:

### 1. SSL/TLS Encryption

Ensure your website has an SSL certificate, which encrypts data transmitted between the user’s browser and your website. This is vital for protecting any information exchanged during the checkout process.

If using Cloudflare, you can easily enforce TLS 1.2 or higher.

### 2. Implement Strong Authentication and Access Controls

This includes the following measures:

### 3. Use Fortress to Secure Your Website

Fortress can help you dramatically increase the security of your website in ways that directly assist with your PCI compliance. Fortress can:

Plus, a great deal more. Learn more about Fortress here:

A Beginners Guide to Fortress

### 4. Make Use of GridPanes Security Features

GridPane offers a suite of security features that can be employed to keep your website secure. These include:

We also recommend Cloudflare and making use of their free firewall rules to add even more security to your websites.

Learn more about how to secure your websites with GridPane in our case study here:

Security Case Study: Securing 2 Banking Websites Built on WordPress

### 5. Data Center Security

Check your server provider for their data center-specific PCI-DSS compliance information and ensure you host your website in a qualified data center.

### 6. Monitor Transactions and Enable Alerts

Regularly review transactions for any suspicious activity. Both Stripe and PayPal offer tools to help monitor and flag unusual behavior and allow you to enable notifications for potentially fraudulent transactions, account access, or other security-related activities.

### 7. Utilize Stripe and PayPal’s Security Features (if applicable)

Take advantage of the fraud detection and prevention tools offered by Stripe or PayPal, such as machine learning-based fraud detection.

### 8. Educate and Train Staff

Train your employees on basic cybersecurity practices, such as recognizing phishing attempts, maintaining secure access to systems, and ensuring they know how to handle sensitive information.

### 9. Regularly Review and Update Security Policies

Periodically review your security policies and practices to ensure they are up-to-date with the latest standards and recommendations, including any changes in PCI compliance requirements (even if you’re not directly processing cardholder data).

 

## Additional Resources

Below are some additional resources on PCI compliance:

### Qualified Security Assessors

Qualified Security Assessor (QSA) companies are independent security organizations that have been qualified by the PCI Security Standards Council to validate an entity’s adherence to PCI DSS. You can find a list of approved vendors here:

PCI Security Standards Council: Qualified Security Assessors

 

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

