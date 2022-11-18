---
title: Endpoint settings
category: API
---

You can add and update API endpoints on the [API screen](/docs/management/api-list/). Setting up endpoints allows you to manipulate the target resources for clients to access Kuroco's data.

This section describes endpoint configurations in detail.

## Creating an endpoint
On the endpoint list screen, click [Configure endpoint] to open the endpoint configuration dialog.

[![fetched from Gyazo](https://rcms.g.kuroco-img.app/files/user/gyazo/8a429878d26e9e45d5ce658bcbb19283.png?width=600)](https://rcms.g.kuroco-img.app/files/user/gyazo/8a429878d26e9e45d5ce658bcbb19283.png)

![Configure Endpoint dialog](https://rcms.g.kuroco-img.app/files/user/gyazo/59a4cf1984f058dad408732a206cb0d5.png?width=600)

|Item   |Description  |
| :--- | :--- |
|Path| Follows the fixed format of: `/rcms_api/{api_id}/`. The first part of the part, /rcms_api/xxx/, cannot be changed.<ul><li>In general, you should name the path based on how the endpoint is used, such as based on "model + behavior".<br/>For example, `login`, `content/news`, `member/insert`.</ul></li>|
|Model| See: [Model categories](#model-categories) for a detailed description of each category/model/operation.<br/><span style="color:red;">Values such as "v1" in the dropdown menu next to the model type indicate the version of each API model.</span>|
|Summary| Overview of the API. This information will be displayed on the endpoint list/Swagger UI screen.|
|Description| Detailed description of the API, including how to use it, if necessary. This information will be displayed for each endpoint on the Swagger UI screen.<br/>The [CommonMark](https://commonmark.org/help/) notation can be used here. | 
|Authentication| Select the type of authentication:<ul><li>None</li><li>GroupAuth</li><li>MemberCustomSearchAuth</ul></li>If "GroupAuth" or "MemberCustomSearchAuth" is selected, the logged-in user is subject to a permission check when using the API, and the request will be allowed only if there is a match.|
|Cache| The cache period of the API response in seconds. The cache will be automatically cleared when the retrieved data (such as contents or members) is updated.<br/>(Note: Since Kuroco is a pay-per-use service, we recommended that you configure the cache for media sites or other applications where a large number of requests are expected. We recommend a cache period of 1 day, 1 week, etc.) |

## Model categories

This section explains the category list for the "Model" field.

[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/f13316e8fc045e873186c9064dad3f7f.png?width=600)](https://rcms.g.kuroco-img.app/files/user/gyazo/f13316e8fc045e873186c9064dad3f7f.png)

### Authentication
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Login|login_challenge|Login|
||token|Get access token|
||logout|Logout|
||reminder|Send password reset e-mail / resets password<br/>(when the user has forgotten their current password)|
||reset_password|Change current password<br/>(when the user remembers their current password)|
||profile|Get login user information|
||gcs_info|Get information about the site-integrated GCS (Cloud Storage for Firebase)|
||firebaseToken|Get the authentication token of the site-integrated Firebase|

### Content
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Topics|list|Get content list|
||details|Get content details|
||preview|Get a preview of the content|
||insert|Add new content|
||update|Update current content|
||delete|Delete current content|
|TopicsCategory|list|Get category list|
|TopicsGroup|list|Get content definition list|
||details|Get content definition details|

### Member
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|MemberProvisional|list|Get pre-member list|
|Member|list|Get member list|
||details|Get member details|
||invite|Invite a member|
||insert|Add new member|
||update|Update current member|
||delete|Delete current member|
||bulk_upsert|Add/update members in bulk|
|MemberCustomSearch|list|Get custom member filter list|
||details|Get custom member filter details|
||insert|Add new custom member filter|
||update|Update existing custom member filter|
||delete|Delete existing custom member filter|
||identify|Get custom member filter that match the member information|
|MemberForm|details|Get member item settings details|
|MemberGroup|list|Get group list|

### Activity
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Comment|list|Get comment list|
||insert|Add new comment|
||update|Update current comment|
||delete|Delete current comment|

### Favorite
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Favorite|list|Get favorite list|
||insert|Add new favorite|
||delete|Delete current favorite|

### Inquiry
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|InquiryMessage|list|Get inquiry response list|
||details|Get inquiry response details|
||send|Send inquiry response|
||update|Update inquiry response|
||delete|Delete inquiry response|
||InquiryForm|list|Get inquiry information list|
||details|Get item information for each form|
||insert|Add new item information for each form|
||update|Update current item information for each form|
||delete|Delete current item information for each form|
||report|Get response report for each form|

### Notification
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Magazine|send|Send notification|

### E-commerce
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|ECCart|details|Get cart details|
||add|Add products to cart|
||update|Update products in cart|
||ECPayment|list|Get payment method list|
||details|Get payment method details|
||ECOderSubscription|list|Get subscription order list| 
||details|Get subscription order details|
||insert|Add subscription order|
||ECDelivery|list|Get delivery list|
||details|Get delivery details|
|ECShop|list|Get shop list| 
||details|Get shop details|
|ECProduct|list|Get product list|
||details|Get product details|
|ECOrder|list|Get order list|
||details|Get order details|
||total|Get order totals|
||purchase|Purchase goods|
||cancel|Cancel order|
||insert|Add new order information|

### Files
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Files|upload|Upload files|

### Tags
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Tag|list|Get tag list|
||insert|Add new tag|
||delete|Delete existing tag|
|TagCategory|list|Get tag category list|

### Tables
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Master|list|Get contents of table (master)|
||insert|Add new table (master)|
||update|Update current table (master)|
||delete|Delete current table (master)|

### Asynchronous processing
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Batch|webhook|Call a batch process|
||list|Get batch process list|
||check_batch|Get batch process status|

### API
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Api|bulk|Batch API endpoint execution|
||list|Get API list|
||openapi_data|Get openapi.json for the API|
||request_api|Execute the API created by the custom function (GET method)|
||request_api_post|Execute the API created by the custom function (POST method)|
||add_site|Add new Kuroco site|

### Workflow
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Approvalflow|review|Approve or reject pending workflow data|
||list_pending|Get a list of pending workflow data|
||pending_detail|Get details of pending workflow data|

### Payments
|Model   |Operation   |Description  |
| :--- | :--- | :--- |
|Stripe|checkout|Subscription payment URL creation|
||cancel_order|Cancel subscription|
