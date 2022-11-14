---
title: Integrating and setting up subscription billing with Stripe
description: The Stripe screen enables you to configure settings for integrating Stripe into your website.
---

## Overview

This tutorial explains how to integrate Stripe into Kuroco and set up recurrent billing for a fixed-price product.

## What you'll learn

The flow for the whole setup process is divided into three parts:

* [Integrating Stripe into Kuroco](#stripe-integration)
  - [Getting the API keys from Stripe](#obtaining-api-keys-from-stripe)
  - [Creating a webhook in Stripe](#creating-your-webhook-in-stripe)
  - [Integration setup in Kuroco](#integrating-stripe-into-kuroco)

* [Adding your product(s)](#adding-your-products)
  - [In Stripe](#stripe)
  - [In Kuroco](#kuroco)

* [Setting up the API](#api-setup)
  - [Creating a checkout and a cancellation endpoint](#endpoint-configuration)
  - [Verifying the checkout endpoint](#verifying-the-billing-process)
  - [Verifying the cancellation endpoint](#verifying-the-subscription-cancellation)


## Before you start

Before starting the Stripe integration, we recommend reading [Second tutorial - Overview](#link) to get a general understanding of how Stripe payment processing works in Kuroco.


## Stripe integration

First, you will need to obtain the API keys and webhook from Stripe and enter them into you Kuroco admin panel.

### Obtaining API keys from Stripe

1. In your browser, go to the [Stripe dashboard](https://dashboard.stripe.com/) and select your mode ("Developer" or "Test mode") in the upper right corner.
2. On the next page, select [API keys] in the left sidebar menu.     
3. You will see the [Publishable key] and the [Secret key]. Note them down for later use.

<!-- [![Image from Gyazo](https://t.gyazo.com/teams/diverta/0c690e9687ed4e419ac44c859b8831e6.png)](https://diverta.gyazo.com/0c690e9687ed4e419ac44c859b8831e6) -->

[[info]] It is important to select the correct mode for your purposes ("Developer" or "Test mode") when performing your integration, as they have different API keys. If you need to switch modes, make sure to copy the keys again and update them in your Kuroco admin panel.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/ec2dbef4271532d54405311499d2889c.png)](https://diverta.gyazo.com/ec2dbef4271532d54405311499d2889c)

### Creating your webhook in Stripe

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/3c8abbd3fc861a4a343b3ca590460d7f.png)](https://diverta.gyazo.com/3c8abbd3fc861a4a343b3ca590460d7f)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/94aa9e09dd6d2d44b2a63a57b92cdc06.png)](https://diverta.gyazo.com/94aa9e09dd6d2d44b2a63a57b92cdc06)
-->

1. Next, select [Webhooks] in the side menu. On the Webhooks page, click [Add an endpoint].
2. You will be redirected to the webhook configuration page, where you will add a webhook that allows Kuroco to determine if the Stripe payment was successful.
3. Set up your webhook as follows:

| Field        | Value                                                                      |
| :---         | :---                                                                               |
| Endpoint URL | Enter the endpoint URL found on the [Kuroco Stripe screen](https://t.gyazo.com/teams/diverta/964b549bd5a684ad32048d4e6f80e72b.png). |
| Description  | Enter a description for your webhook. |
| Listen to    | Select [Events on your account].                                                    |
| Version      | Select the latest current version of your account.                                 |
| Events       | Click [+ Select events] and select the following events from the dropdown list:<ul><li>`customer.subscription.created`</li><li>`customer.subscription.deleted`</li><li>`customer.subscription.updated`</ul></li>Click [Add events] when you are done. |

4. When you are done, click [Add endpoint] to add the new endpoint to your Stripe dashboard.
5. After you have added your endpoint, click [Reveal signing secret] to see the webhook secret. Copy it for later use.

### Integrating Stripe into Kuroco

1. In Kuroco's left sidebar menu, under “SETTINGS”, select [External system integration] -> [Stripe].   
2. On the Stripe integration screen, enter the keys you copied from Stripe UI in the corresponding fields.

| Field           | Value                                      |
| :---            | :---                                       |
| Status          | Select "Enable".         |
| Publishable key | Enter the publishable key you copied.          |
| Secret key      | Enter the secret key you copied.               |
| Webhook secret  | Enter the signing secret you copied.           |

3. When you are done, click [Update] to apply these changes.

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/4f920429811751b809043c3eaeaefe4c.png)](https://diverta.gyazo.com/4f920429811751b809043c3eaeaefe4c)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/d2d1503862df4a5e06adbb3bc0610128.png)](https://diverta.gyazo.com/d2d1503862df4a5e06adbb3bc0610128)
-->

## Adding your product(s)

The next step is to add your product(s) in Stripe and in Kuroco.    

### Stripe

1. In the top bar menu, click [Products].    
2. Then, select [All products] from the left sidebar.    
3. On the Products page, click [+ Add a product].
4. You will be redirected to the Add product page. Fill in the details of your product as follows. For more information, refer to the [Stripe docs: Manage products and prices](https://stripe.com/docs/products-prices/manage-prices).

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/1aefcbb50634fb03981076f1e6b47033.png)](https://diverta.gyazo.com/1aefcbb50634fb03981076f1e6b47033)
-->

| Field          | Description                                                              |
| :---           | :---                                                                     |
| Name           | Name of the product.                                                     |
| Description    | Brief information of the product.                                     |
| Pricing        | Select [Standard pricing].                                            |
| Recurring      | Select [Recurring].                   |
| Billing period | Select your billing period (interval of time between each statement). |

5. When you are done, click [Save product] to add your product to the Stripe database.
6. You will be redirected to the Details page. Under "Pricing", find the API ID and copy it for later use.

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/d25df95fe43ed69f9fa8eaa6d7111fb2.png)](https://diverta.gyazo.com/d25df95fe43ed69f9fa8eaa6d7111fb2)
-->
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/f5dd7ab131ccb3607d2d6ab11fcb150e.png)](https://diverta.gyazo.com/f5dd7ab131ccb3607d2d6ab11fcb150e)

7. To add another product, repeat the above steps under "[Adding your product](#adding-your-product)".

### Kuroco

1. Next, go to your Kuroco admin panel and create an empty member group for your product. If you have more than one product, each product should have a separate group.    
[[info]] Note: For a tutorial on how to create new groups, see [Creating groups](/docs/tutorials/how-to-make-new-group/).

2. From the group list, click the name of the group you just created to edit it.
3. On the Group editor screen, enter the API ID you copied from Stripe into "Stripe price ID".

[[info]] Note: The "Stripe price ID" field will only appear after you have successfully integrated Stripe into your Kuroco admin panel. If you do not see this field, go back to the integration step above and verify if all your inputs and settings are correct.

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/e81e5bf8059255990282938646463d7f.png)](https://diverta.gyazo.com/e81e5bf8059255990282938646463d7f)
-->
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/78f1935551a531aca28173a429c81e57.png)](https://diverta.gyazo.com/78f1935551a531aca28173a429c81e57)

When a member completes checkout from the payment page, they will be automatically added to this product group.

## API setup

The final step is to add and verify the required endpoints for the payment process.    
You will need two endpoints: a checkout endpoint and a cancellation endpoint. They will be used to process payments and cancel subscriptions, respectively.

<!-- EXPLANATION PROBABLY NOT NEEDED (?)
Calling either endpoint returns a JSON response containing the relevant Stripe URL. You would then direct the user to the checkout page to enter their payment details and authorize the transaction.
-->

### Endpoint configuration

[[info]] To use the payment functionality, you must use cookies or dynamic tokens as your API security settings.

<!--
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/e806f56c501dd75139ed612381965027.png)](https://diverta.gyazo.com/e806f56c501dd75139ed612381965027)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/060b0e609139f239dfa426948319ca16.png)](https://diverta.gyazo.com/060b0e609139f239dfa426948319ca16)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/796d39132dc9ec8b7968d3a29d26627b.png)](https://diverta.gyazo.com/796d39132dc9ec8b7968d3a29d26627b)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/d1589b7116a2815675a1112ce1a49378.png)](https://diverta.gyazo.com/d1589b7116a2815675a1112ce1a49378)
-->

1. In Kuroco's left sidebar menu, click [API] and select the API where you will be adding the endpoint.
2. On the endpoint list screen, click [Add new endpoint]. 
3. In the Endpoint settings dialog, enter the following:

| Field | Value |
| :--- | :--- |
| Category | Payments |
| Model | Stripe, v1 |
| Operation | checkout(\*) |
| products_list  | Enter the price ID (Stripe API ID) of the product.<ul><li>Note: You can add multiple products to a single checkout.</li><li>Note: You can not change the price ID from the front end</li></ul> |
| return_url     | Front-end URL for the payment success page. |
| return_err_url | Front-end URL for the payment failure page. |

[[info]] \*For the cancellation endpoint, select [cancel_order] for "Operation".

4. When you are done, click [Add] to save the endpoint.


### Verifying the billing process

<!-- VIDEO: [![Image from Gyazo](https://t.gyazo.com/teams/diverta/405f30e1cfcef72cede37b86a45d1335.gif)](https://diverta.gyazo.com/405f30e1cfcef72cede37b86a45d1335) 
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/03fdaee9d13b521b773e7aed365d83e0.png)](https://diverta.gyazo.com/03fdaee9d13b521b773e7aed365d83e0)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/cc0926ce21366db86a5a545014dfe375.png)](https://diverta.gyazo.com/cc0926ce21366db86a5a545014dfe375)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/13a558163253ed7b19acf9805a2898a6.png)](https://diverta.gyazo.com/13a558163253ed7b19acf9805a2898a6)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/e00d97f4fa571111e43c869924f2eba5.png)](https://diverta.gyazo.com/e00d97f4fa571111e43c869924f2eba5)
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/0029537b14a95543876fc455a60b3a91.png)](https://diverta.gyazo.com/0029537b14a95543876fc455a60b3a91)
-->

To check if your billing process is working as expected, verify the endpoint response from the Swagger UI and make a test payment.

1. From the sidebar menu, select the API containing your checkout endpoint. On the endpoint list screen, click [Swagger UI].
2. On the Swagger UI screen, select your checkout endpoint and click [Try it out].
3. Scroll down and click [Execute].
4. Copy the URL in the response body.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/bd0480d5b7ba9a21dd703119387b99ac.jpg)](https://diverta.gyazo.com/bd0480d5b7ba9a21dd703119387b99ac)

5. Access the URL in your browser. You should see the payment screen below. Enter your payment details and click [Subscribe].

[[info]] You can use [test cards](https://stripe.com/docs/testing#international-cards) to simulate various scenarios.  

6. If the payment was successful, you will be redirected to the payment success page you set in your endpoint.

<!--
Stripe-side verification steps needed
-->

Once completed, the member is automatically added to the member group(s) for the product(s). They will also automatically receive a Stripe member ID and subscription ID attached to their Kuroco account. For more details, see [Second tutorial - Customer ID & Subscription ID](#link).


### Verifying the subscription cancellation

<!--
To test the cancellation process, go to the Swagger UI and click [Try it out] for your cancellation endpoint. 

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/8b00ca3d85afb619f21e465a4c58f176.png)](https://diverta.gyazo.com/8b00ca3d85afb619f21e465a4c58f176)

Scroll down and click [Execute].

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/e9e79640827b9df7295d00da4803c7f7.png)](https://diverta.gyazo.com/e9e79640827b9df7295d00da4803c7f7)
-->

To test the cancellation process, repeat checkout verification steps 1 - 3 for the cancellation endpoint. The member will be automatically removed from the associated products, and their Stripe subscription ID will be automatically unlinked from their Kuroco account. For more details, see [Second tutorial - Customer ID & Subscription ID](#link).

[[info]] Note that subscriptions are canceled immediately without redirecting to a confirmation page. 


## More information

Below are some points to take note of when setting up subscription billing with Stripe in Kuroco.

### Limitations

Currently, Kuroco does not support the following payment types with Stripe:
- Guest checkout (i.e., non-logged-in users)
- One-time purchases
- Multiple subscriptions\*

<!-- TO BE ADDED
[[info]] \*Note: For more information, see [Second tutorial](#link) or contact our [Support Team](https://kuroco.zendesk.com/hc/en-us).
-->


### Stripe CLI

You can also use the [Stripe CLI](https://stripe.com/docs/stripe-cli) developer tool to test your payment function by listening for real-time event changes such as new subscriptions, updates, and payment processing on your Stripe account.

To do this, run the command `stripe listen` with the commonly used flags listed below. You will receive a webhook secret, which you can add to your local environment to decrypt the information.

| Flag          | Description                                                                    |
| :---          | :---                                                                           |
| --forward-to  | Enter the your localhost URL to which you want to forward the webhook calls.   |
| --events      | Enter a comma-separated list of events you want to listen for.<ul><li>You can find the list of events on your [Stripe webhook page](#creating-your-webhook)</ul></li> |
| --skip-verify | Use this flag if you do not have a local SSL certificate or it is invalid. |

For further details about using the Stripe CLI, see:
- [Stripe Docs: Get started with the Stripe CLI](https://stripe.com/docs/stripe-cli)
- [Stripe Docs: Listen for events with the Stripe CLI](https://stripe.com/docs/stripe-cli/about-events)
<!-- TO BE ADDED
- [Second tutorial on managing subscriptions/products/customers](#link)
-->
