---
title: Bulk uploading using the `bulk_upsert` endpoint
description: bulk_upsert is an API operation to update multiple contents in bulk. This tutorial explains how to import CSV file in random formats to a content using it.
---

`bulk_upsert` is an API operation to update multiple contents in bulk. 
This tutorial explains how to import CSV file in random formats to a content using it.

## Prerequisite

The CSV file is imported based on the following conditions:

1. The CSV file is imported manually to KurocoFiles.
2. The import process is executed by batch at 12:00AM everyday by batch.
3. The import process will be executed if there are any file updates between the previous batch process and the start of next one.
4. Updating the existing contents and adding non-existing ones.
5. The CSV file to be uploaded is saved in UTF-8 letter code.

## Prepare a CSV file

First, prepare the CSV data to be imported. This time, we will use the following list of mobile devices.

| item_number | item_name | category | description | status | item_color | release_date | is_public |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 00000001 | SmartPhone | SP | Smartphone | 1 | black,white,red,blue | 2020/12/10 | TRUE |
| 00000002 | SmartPhone Lite | SP | popular edition Smartphone | 1 | black,white | 2021/12/10 | TRUE |
| 00000003 | Tablet | TB | Tablet | 0 | silver | 2020/1/15 | FALSE |
| 00000004 | Tablet 2 | TB | Tablet (2nd gen) | 1 | silver | 2022/1/15 | TRUE |

The item definition of each column is as follows.

| Item name | Item content | Value |
| :-- | :-- | :-- |
| item_number | Item number | Unique 8 digit number in each item |
| item_name | Item name | any text |
| category | Item category | text<br/>SP: Smartphone<br/>TB: Tablet |
| description | Item description | any text |
| status | Sales status | number <br/>0: sale ended<br/>1: on sales |
| item_color | Item color | Text (Multiple values can be set by separating with commas)<br/>black:black<br/>white<br/>silver<br/>red<br/>blue |
| release_date | Release date | date (yyyy/mm/dd) |
| is_public | public/private | text<br/>TRUE: public<br/>FALSE: private |

## Set content structure

### 1. design an item
In order to be able to import each row of CSV as content, first we design the content definition items.  

If there is a corresponding default item, use the default item.  
Otherwise, map to extension items and set Slug with the same name as the CSV item.

| CSV Item name | Kuroco Item name(admin screen) | KurocoItem name(API) | Item format  | Description |
| :-- | :-- | :-- | :-- | :-- |
| item_number | Slug | slug | - | Used when sending requests to bulk_upsert endpoint.<br/>The original item is in numeric format, but the Slug needs to have a textual value, so prefix it like this:<br/>`ITEM-%%item_number%%` |
| item_name | title | subject | - |  |
| category | category | contents_type | - |  |
| release_date | date | ymd | - |  |
| is_public | public setting | open_flg | - |  |
| item_number | extension item1 | item_number | Single-line text | We also map the same items to Slug, but here we set the original value without the prefix. |
| description | extension item 2 | description | Multi-line text |  |
| status | extension item 3 | status | Dropdown selection | Options:<br/>`0::Sales ended`<br/>`1::On sales` |
| item_color | extension item 4 | item_color | multiple choice | Options:<br/>`black::black`<br/>`white::white`<br/>`silver::silver`<br/>`red::red`<br/>`blue::blue` |

### 2. Create content group

After designing the content structure, we create a new topic group.  
Please check [Creating topic group(s)
](/docs/tutorials/adding-a-topics/)for the detail of how to create it.  

First, set as follows. For other items, leave the default settings.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/9530ede292aaef83cc7fcd2d42d8f29f.png)](https://diverta.gyazo.com/9530ede292aaef83cc7fcd2d42d8f29f)  

| Item name | Value | Description |
| :-- | :-- | :-- |
| Name | mobile device |  |
| Do not leave update history | Enable | Improves performance instead of leaving no update history.<br/>If it is necessary to update the data every day, it is recommended to enable it. |

Next, we set the extension item as defined in "1. Design the item".

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/56b5678aa6f0474b9c7dc70cf37da7b5.png)](https://diverta.gyazo.com/56b5678aa6f0474b9c7dc70cf37da7b5)

After completing the above settings, click the [Add] button to add a new topics group.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/0a14165c6cace056e733b6a10baed4d6.png)](https://diverta.gyazo.com/0a14165c6cace056e733b6a10baed4d6)

### 3. Create categories

Finally, create categories for your content so that you can categorize your items. 
Please refer to [Content category](/docs/management/content-structure-topics-category/) for the detail.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/1b9b3a0964d14bf06875cc69ca4785a2.png)](https://diverta.gyazo.com/1b9b3a0964d14bf06875cc69ca4785a2)

| category ID | category name | Field 01 |
| :-- | :-- | :-- |
| 1 (Auto numbering) | Smartphone | SP |
| 2 (Auto numbering) | Tablet | TB |

Since categoryID is automatically numbered when creating a new category, please replace it with the value set in your own environment.  
For `field 01`, set the category value of the import source CSV.

## Set the member who execute the backend processing
We set the member who execute the backend processing.The member ID set here will be used when describing batch processing later.

### Create a new member

Access the [member editor](/docs/management/member/#member-editor) page and add a member who will execute the backend processing.  
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/51789df8453c8e6900ce37a90f5b360c.png)](https://diverta.gyazo.com/51789df8453c8e6900ce37a90f5b360c)

| Item name | Value | Description |
| :-- | :-- | :-- |
| Name | system admin | Set a value that makes it easy to identify that it is for backend use. |
| Login ID | system | Set a value that makes it easy to identify that it is for backend use. |
| Password | (any password) | Set a strong password that you do not use elsewhere. |
| Group | Admin | Set a group whose user type is "superuser". This time, we will use the group (group ID: 1) that exists by default when the site is created. |

### Set constants

Access the [constants](/docs/management/constants/) screen and set constants to be referred from the batch processing.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/06ccf1b3b18a25a19a3e8eeb0cfe0553.png)](https://diverta.gyazo.com/06ccf1b3b18a25a19a3e8eeb0cfe0553)  

| Item name | Value | Description |
| :-- | :-- | :-- |
| Name | SYSTEM_MEMBER_ID |  |
| Value | (Member ID) | Set the ID of the newly created member. Since the ID is automatically numbered, please replace it with the value set in your own environment. |

## Configure API

### Create API

Access the [API](/docs/management/api-list/) screen and create a new API to set the endpoint for backend processing.  

[[info]]Mixing endpoints with different purposes (for front-end, back-end, etc.) in the same API complicates authentication settings.
Since this may increase security risks, it is recommended to separate the API settings by usage.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/1dc3002c34eb9d712ff5e158cf3e0de4.png)](https://diverta.gyazo.com/1dc3002c34eb9d712ff5e158cf3e0de4)

| Item name | Value | Description |
| :-- | :-- | :-- |
| title | Internal API | Set a value that makes it easy to identify that it is for backend use. |
| version | 1.0 |  |
| description | Internal API for Backend Process |  |

After creating the API, click [Security], select [Dynamic Access Token], and save.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/afbae4943c2c1e93f6cfae6e527f0182.png)](https://diverta.gyazo.com/afbae4943c2c1e93f6cfae6e527f0182)

### Add API endpoint

Click the [Add new endpoint] button to add the bulk_upsert endpoint to the API you just set up. 

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/7b423a69ccff0c059738fdda16713c70.png)](https://diverta.gyazo.com/7b423a69ccff0c059738fdda16713c70)

| Item name | Value | Description |
| :-- | :-- | :-- |
| Path | mobile_devices/bulk_upsert |  |
| Model | categoryー: Content<br/>Model: Topics (v1)<br/>Operation: bulk_upsert |  |
| API request restriction | GroupAuth (Admin) | Set a group that the member created previously at [Create a new member](#create-a-new-member) belongs to. |

For the basic settings and advanced settings, set the following values.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/b0f40c599f4b58e100926182ef913f3e.png)](https://diverta.gyazo.com/b0f40c599f4b58e100926182ef913f3e)  

| Parameter name | Value | Description |
| :-- | :-- | :-- |
| topics_group_id | 12 | ID of the topics group to be updated. Set the ID numbered to the topics group "mobile device" created previously. |
| id_reference_allow_list | slug | Set items that can be specified as keys when updating content. Detail is explained below. |
| ignore_errors | true | Ignores rows with validation errors and add/update only valid content. |

**Regarding id_reference_allow_list parameter**

When updating existing content with the bulk_upsert API, you need to specify the `topics_id` which is the key to identify the target content. Normally, we specify the number automatically assigned by Kuroco as follows.
```
{
    "topics_id": 1,
    "slug": "ITEM-00000001",
    "subject": "Smartphone",
    ...
}
```

The problem here is how to identify the `topics_id` to be updated.  

For other items, values can be converted from the CSV file, but `topics_id` is data held only by Kuroco. In order to identify this value, it is necessary to call the list API in advance to obtain the existing content. However, implementing this has the following problems:

- Program gets complicated
- Process time increases

`id_reference_allow_list` is a parameter prepared to solve the above. If it is set, you can add or update content using any item as a key instead of topics_id. For example, if `slug` is set like this time, the following requests can be specified.

```
{
    "topics_id": "slug",
    "slug": "ITEM-00000001",
    "subject": "Updated Title",
    ...
}
```

If the above data is sent, if the content of `slug = "ITEM-00000001"` already exists, it will be updated, otherwise it will be newly added. This makes it possible to add content using only the ID of the original data without considering the `topics_id` numbered by Kuroco.

## Implement batch process

Using the settings set up so far, we will implement batch process that executes daily import.  

First, access the [Batch editor](/docs/management/batch/#batch-editor) screen and enter the following contents.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/ef837bb2c38b9d5640036c85073b2f17.png)](https://diverta.gyazo.com/ef837bb2c38b9d5640036c85073b2f17)

| Item name | Value |
| :-- | :-- |
| title | upsert_mobile_devices |
| Identifier | upsert_mobile_devices |
| Batch | Every day/00:00 |

After entering above, enter the following code in the `Process` field and click [Add].  

```smarty
{*
    Pre-processing
*}
{* Authenticate using the member ID set in the constant *}
{login member_id=$smarty.const.SYSTEM_MEMBER_ID overwrite=true}

{* Check if CSV file is placed *}
{assign var='uploaded_csv_path' value='/files/ltd/bulk_upsert/mobile_devices.csv'}
{if !$uploaded_csv_path|rcms_file_exists}
    {logger msg1='upsert_mobile_devices' msg2='CSV file is not found'}
    {return}
{/if}
{* Check the update date and time of CSV file *}
{assign var='csv_updated_at' value=$uploaded_csv_path|rcms_file_mtime}
{if $csv_updated_at < '-1 day 0:00:00'|strtotime}
    {logger msg1='upsert_mobile_devices' msg2='CSV file is not updated'}
    {return}
{/if}

{* %% bulk_upsert %% *}
```

Next, replace the commented part `{* %% bulk_upsert %% *}` in the code above with the actual content update process.

First, access the [Swagger UI](/docs/management/api-list/#swagger-ui) screen and select the endpoint `mobile_devices/bulk_upsert` created previously.  

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/56913274f0c4421ce4de7fe8795a1481.png)](https://diverta.gyazo.com/56913274f0c4421ce4de7fe8795a1481)

Click [Request body] -> [Schema] to see the definition of the request body accepted by the bulk_upsert endpoint.  

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/72daafababe90bb2cc6298c900fd3954.png)](https://diverta.gyazo.com/72daafababe90bb2cc6298c900fd3954)

The bulk_upsert API accepts request bodies in the following two formats.
This time, we will proceed with processing using the JSON format.

<!-- CSVの処理での説明ができたら文言変更-->
<!--生成すべき値が形式ごとに異なるため、それぞれの処理について説明します。
-->

| Format | Request body |
| :-- | :-- |
| JSON |`{"list": [{...}]}` |
| CSV file | `{"file": {...}, "encoding": "..."}` |


### When updating in JSON format

You can see a detailed definition of each item by expanding the `list` property from the Request body schema.  

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/6f1d5a6891f8cd3016327ba107119640.png)](https://diverta.gyazo.com/6f1d5a6891f8cd3016327ba107119640)

Comparing the above schema with the items we are updating, we can see that the request body should look something like this:

```js
{
    "list": [
        {
            "topics_id": "slug",
            "slug": "ITEM-00000001",
            "subject": "SmartPhone",
            "contents_type": 78,
            "open_flg": 1,
            "ymd": "2020-12-10",
            "item_number": "00000001",
            "description": "Smartphone",
            "status": "1",
            "item_color": ["black", "white", "red", "blue"]
        },
        {
            "topics_id": "slug",
            "slug": "ITEM-00000001",
            // ...
        },
        // ...
    ]
}
```

Now that we know the format of the request body to pass to the endpoint, we can implement batch process. Add the following code to the batch process created earlier and click the [Update] button.

```smarty
{*
    Initiate necessary constants
*}
{* json body ({"list": []}) passed to bulk_upsert endpoint *}
{assign_array var='bulk_upsert_body'      values=''}
{assign_array var='bulk_upsert_body.list' values=''}

{assign_array   var='csv_header' values=''}{* CSV header ([]) *}
{assign         var='chunk_unit' value=1000}{* Unit for split upload *}

{*
    Get the total number of rows of CSV to be processed in advance
*}
{assign var='last_index' value=-1}
{read_file name='uploaded_csv' row='csv_row' type='csv' path=$uploaded_csv_path}
    {assign var='last_index' value=$last_index+1}
    {logger msg1="last_index取得処理" msg2=$last_index}
{/read_file}

{*
    Update process
*}
{* index indicating the row being processed *}
{assign var='i' value=0}
{* Read CSV file *}
{read_file name='uploaded_csv' row='csv_row' type='csv' path=$uploaded_csv_path}
    {if !$csv_row|@is_array}
        {logger msg1='upsert_mobile_devices' msg2='Invalid csv row' msg3=$csv_row}
    {elseif $i === 0}
        {* Get CSV header *}
        {assign var='csv_header' value=$csv_row}
        {$csv_header|@rcms_json_encode}
        {logger msg1="CGet CSV header" msg2=$csv_row}
    {else}
        {logger msg1="Get CSV header"}
        {* CSV行の変換 *}
        {assign_array var='topics'           values=''}
        {assign       var='topics.topics_id' value='slug'}{* add/update slug as key *}
        {foreach from=$csv_row key='k' item='v'}
            {assign var='col_name'   value=$csv_header[$k]}{* Get CSV Item name *}
            {if     $col_name == 'item_number'}
                {* Product no. *}
                {assign var='topics.slug'        value="ITEM-`$v`"}
                {assign var='topics.item_number' value=$v}
            {elseif $col_name == 'item_name'}
                {* Item name *}
                {assign var='topics.subject' value=$v}
            {elseif $col_name == 'category'}
                {* category *}
                {if     $v == 'SP'}
                    {assign var='topics.contents_type' value=78}
                {elseif $v == 'TB'}
                    {assign var='topics.contents_type' value=79}
                {/if}
            {elseif $col_name == 'item_color'}
                {* color *}
                {assign var='topics.item_color' value=','|explode:$v}
            {elseif $col_name == 'release_date'}
                {* release date *}
                {strtodate var='topics.ymd' format='Y-m-d' timestamp=$v}
            {elseif $col_name == 'is_public'}
                {* public/private *}
                {if $v == 'TRUE'}
                    {assign var='topics.open_flg' value=1}
                {else}
                    {assign var='topics.open_flg' value=0}
                {/if}
            {else}
                {* Others *}
                {assign var="topics.`$col_name`" value=$v}
            {/if}
        {/foreach}
        {* Add to JSON body ({"list": [..., {...}]}) *}
        {assign var='bulk_upsert_body.list.' value=$topics}
    {/if}
    {* Update by dividing for each number defined in $chunk_unit *}
    {if $bulk_upsert_body|@count === $chunk_unit ||
        ($i === $last_index && $bulk_upsert_body|@count > 0)}
        {* Request to bulk_upsert endpoint (Add _async=true parameter and execute in batch process) *}
        {api_internal
            var='bulk_upsert_response'
            status_var='bulk_upsert_status'
            endpoint='/rcms-api/8/mobile_devices/bulk_upsert?_async=true'
            method='POST'
            queries=$bulk_upsert_body
            member_id=$smarty.session.member_id}
        {* Output to log if failed *}
        {if !$bulk_upsert_status || $bulk_upsert_response.errors}
            {logger msg1='upsert_mobile_devices' msg2='Request failed' msg3="index: `$i`" msg4=$bulk_upsert_response}
        {/if}
        {* JSON bodyの初期化 ({"list": []}) *}
        {assign_array var='bulk_upsert_body.list' values=''}
    {/if}
    {logger msg1=$i msg2=$last_index msg3=$topics msg4=$csv_row}
    {assign var='i' value=$i+1}
{/read_file}
```

<!-- textlint-disable -->
<!-- 理由:1文の文字数警告がでるがURL部分のせいなので無視 -->

[[info]]
Replace `/rcms-api/8/mobile_devices/bulk_upsert` with your own endpoint.  
Use the category ID in your environment for `{assign var='topics.contents_type' value=78}`、`{assign var='topics.contents_type' value=79}`.
<!-- textlint-enable -->
We supplement the details of the processing.

**About reading CSV files**

`read_file` is a plugin for reading text data line by line. It can be used to read CSV files by specifying `csv` for the `type` parameter.  
The character code that can be read by `read_file` is UTF-8 only.  

```smarty
{read_file name='uploaded_csv' row='csv_row' type='csv' path=$uploaded_csv_path}
    {* ... *}
{/read_file}
```

The CSV row data is assigned to the variable name `$csv_row` specified by the `row` parameter. You can check the contents of the data by writing the following process inside the `{read_file}{/read_file}` block.  

```smarty
{$csv_row|@rcms_json_encode}
```

The following array data is output. The request body is generated by transforming these values based on the field definition.  

```
["00000001", "SmartPhone", "SP", "Smartphone", "1", "black,white,red,blue", "2020/12/10", "TRUE"]
```

**About adding/updating contents**

The `api_internal` plugin is used to call the `bulk_upsert` endpoint for adding/updating content.
<!-- 
TODO: 該当のドキュメントが英訳できしだい以下を追加。

詳しい利用方法については、[オリジナル処理からKurocoのAPIを呼び出せますか？](/ja/docs/faq/how-to-request-kuroco-api-from-smarty-function/)を参照ください。 -->

```smarty
{api_internal
    var='bulk_upsert_response'
    status_var='bulk_upsert_status'
    endpoint='/rcms-api/23/mobile_devices/bulk_upsert?_async=true'
    method='POST'
    queries=$bulk_upsert_body
    member_id=$smarty.session.member_id}
```

The endpoint path has the `_async=true` parameter to execute API processing asynchronously.  

Calls to endpoints are typically synchronous. After submitting the request, you need to wait for the processing to complete. However, since the bulk_upsert API handles a large amount of content at once, depending on the number of CSV data, it may take some time to complete the process, resulting in a timeout.  

If you use the `_async=true` parameter, it will only register the batch process and return the response immediately without executing the addition/update process at the time of the request. The processing of the called API is executed in a separate process from the caller, so timeout issues can be avoided. Specify this when the number of data to be updated is large.  

## Check the operation
Now that the settings have been completed, let's check the operation.  
First, place the CSV file (`mobile_devices.csv`) in the directory (`/ltd/bulk_upsert`) specified by batch processing.　　
Since the KurocoFiles (Private) folder will be `ltd`, create a `bulk_upsert` folder under it and set the CSV file.  

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/9cf8603faace864ed3669f67d9b807e2.png)](https://diverta.gyazo.com/9cf8603faace864ed3669f67d9b807e2)

Next, access the editor screen created previously and click [Run now].  
[![Image from Gyazo](https://t.gyazo.com/teams/diverta/3a1b7c113849f37aa1bbf22013f238e6.png)](https://diverta.gyazo.com/3a1b7c113849f37aa1bbf22013f238e6)

If you check the contents list of "mobile device", you can see that the contents are registered from CSV.  

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/e42398db58721d3da48ea595f8c3de6c.png)](https://diverta.gyazo.com/e42398db58721d3da48ea595f8c3de6c)

Confirmation of operation is completed.

## Related documents
- [Batch](/docs/management/batch/)
- [Constants](/docs/management/constants/)
<!-- - [カスタム処理からKurocoのAPIを呼び出せますか？](/ja/docs/faq/how-to-request-kuroco-api-from-smarty-function/) -->

<!-- todo -->
<!--
### CSVファイル形式で更新する場合
-->
