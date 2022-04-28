---
title: List of additional fields available in the content structure
category: Content
weight: '1'
---

By default, the content editor contains the following 3 fields:

- Topic ID/Slug
- Date
- Title

[](https://diverta.gyazo.com/58ffd2e6c2f2cc9ae7026d9f72ea8b65)

You can set up additional fields using the content structure editor.

See [Content structure - Extended items](/docs/management/content-structure-topics-group/#extended-items) for a detailed guide.

[](https://diverta.gyazo.com/4d054a9b6a1b59344039b26dd344fd79)

Alternatively, click [Settings] to access the settings dialog, where you can define the input restrictions and contents to be displayed.

[](https://diverta.gyazo.com/d33a6204935c6041db2b78ec42b8f7d5)

Configurable contents differ by field (see below).

## List of additional fields

[Text](#%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88)<br> [Text area](#%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%82%A8%E3%83%AA%E3%82%A2)<br> [SelectBox format](#%E9%81%B8%E6%8A%9E%E5%BD%A2%E5%BC%8F)<br> [Image](#%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88)<br> [Multiple choice (check box)](#%E8%A4%87%E6%95%B0%E9%81%B8%E6%8A%9E%E3%83%81%E3%82%A7%E3%83%83%E3%82%AF%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9)<br> [Wysiwyg](#wysiwyg)<br> [Link](#%E9%81%B8%E6%8A%9E%E5%BD%A2%E5%BC%8F)<br> [Date format](#%E6%97%A5%E4%BB%98%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88)<br> [File](#%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB)<br> [Table](#%E8%A4%87%E6%95%B0%E9%81%B8%E6%8A%9E%E3%83%81%E3%82%A7%E3%83%83%E3%82%AF%E3%83%9C%E3%83%83%E3%82%AF%E3%82%B9)<br> [Location](#wysiwyg)<br> [Text (autocomplete)](#%E3%83%86%E3%82%AD%E3%82%B9%E3%83%88%E3%82%AA%E3%83%BC%E3%83%88%E3%82%B3%E3%83%B3%E3%83%97%E3%83%AA%E3%83%BC%E3%83%88)<br> [RelationData SelectBox](#%E9%96%A2%E9%80%A3%E6%83%85%E5%A0%B1%E9%81%B8%E6%8A%9E)<br> [html](#%E6%97%A5%E4%BB%98%E3%83%95%E3%82%A9%E3%83%BC%E3%83%9E%E3%83%83%E3%83%88)<br> [Master format](#%E3%83%9E%E3%82%B9%E3%82%BF%E5%BD%A2%E5%BC%8F)<br> [File manager](#%E3%83%95%E3%82%A1%E3%82%A4%E3%83%AB%E3%83%9E%E3%83%8D%E3%83%BC%E3%82%B8%E3%83%A3)<br> [GCS file](#%E8%A1%A8%E7%B5%84%E3%83%86%E3%83%BC%E3%83%96%E3%83%AB)

<!--[APIフィールド](#apiフィールド)-->

## Text

### Content editor display

[](https://diverta.gyazo.com/2b020827382500d55c16b1e0340edf88)

### Field settings

[](https://diverta.gyazo.com/ba1392b10c24f23116f559b4441e59ff)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
 | Input restriction | Specify the type of string that can be entered.
 | Regular expression | Enter your regular expression here if you selected  this option under "Input restriction" above.
 | Character limit | Enter the minimum and maximum number of characters allowed.

### JSON response

```json
details: {
    "ext_col_XX": "Text",
},
```

## Text area

### Content editor display

[](https://diverta.gyazo.com/d0e13478b3325c54a3d07f862477a42c)

### Field settings

[](https://diverta.gyazo.com/c0f0b14dbece2871d3544338eb4f1d8c)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Width | Set the width of the text area.
 | Height | Set the height of the text area.
 | Character limit | Enter the minimum and maximum number of characters allowed.

### JSON response

```json
details: {
    "ext_col_XX": "Text area",
},
```

## SelectBox format

### Content editor display

[](https://diverta.gyazo.com/43185a1a7a2dd1e1c147cb617117c434)

### Field settings

[](https://diverta.gyazo.com/d4d92f19fc697c4a1525da09a8826f27)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Options | Enter the key for the current option.
　 | Value | Enter the value of the current option.
　 | Default | Check the box to set the current option as the default choice.
　 | Add | Add a new option.
　 | Delete | Delete the current option.

### JSON response

```json
details: {
    "ext_col_XX": {
        "key": "1",
        "label": "Option 1"
    },
},
```

## Image

### Content editor display

[](https://diverta.gyazo.com/94114d049036d27837cfc29231591460)

### Field settings

[](https://diverta.gyazo.com/c5b39a446ba8766eaa74e04184035116)

Field |  |  | Description
:-- | :-- | :-- | :--
Input type | Required |  | Check this box to make the field mandatory.
Extra columns | Extension | Value | Specify the allowed file extension for the upload.
 |  | Add | Add an allowed file extension for the upload.
 |  | Delete | Delete an existing allowed extension.
 | Maximum upload size (MB) |  | Limit the size of images that can be uploaded.
 | Hide caption |  | Check this box to hide the image caption on the content editor screen.

### JSON response

```json
details: {
    "ext_col_XX": {
        "id": "sample_0",
        "url": "https://sample.g.kuroco-img.app/v=1623673449/files/topics/sample.png",
        "desc": ""
    },
},
```

## Multiple choice (checkbox)

### Content editor display

[](https://diverta.gyazo.com/ffdc4592f837335b553e0c0d45635019)

### Field settings

[](https://diverta.gyazo.com/b803ae32fe2918e922fcf988b0950b2c)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Key | Enter the key for the current option.
 | Value | Enter the value of the current option.
 | Default | Check the box to set the current option as the default choice.
 | Add | Add a new option.
 | Delete | Delete the current option.

### JSON response

```json
details: {
    "ext_col_XX": [
        {
            "key": "1",
            "label": "Multiple choice option 1"
        },
        {
            "key": "2",
            "label": "Multiple choice option 2"
        }
    ],
},
```

## Wysiwyg

### Content editor display

[](https://diverta.gyazo.com/ef63db8198ad3b1123ba0724c0866d39)

### Field settings

[](https://diverta.gyazo.com/313957be252c65b85760fa0e218a2c3f)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | vvvvv | vvvvvvvvvvvvvv
 | Width | Set the width of the field.
 | Height | Set the height of the field.
 | Delete plugin | Enter any plugins you wish to remove here.
 | Simple toolbar | Check this box to enable a simplified toolbar display with fewer formatting options.

### JSON response

```json
"details": {
    "ext_col_XX": "<p><strong>Wysiwyg</strong> text area</p>",
},
```

## Link

### Content editor display

[](https://diverta.gyazo.com/336378da627557b9e1c021a7e11ae599)

### Field settings

[](https://diverta.gyazo.com/27cdf0a0a874f8dd63e8738f3e2f6a04)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.

### JSON response

```json
details: {
    "ext_col_XX": {
        "url": "https://kuroco.app/",
        "title": "Kuroco"
    },
},
```

## Date format

### Content editor display

[](https://diverta.gyazo.com/38836415f185cdded83424f406f3466a)

### Field settings

[](https://diverta.gyazo.com/2633ef674ed074922102f7593a0d95ec)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Also include time range (hh:mm) | Check this box to include a time selector in addition to the date.

### JSON response

```json
details: {
    "ext_col_XX":"2021-06-04",
},
```

## KurocoFile

### Content editor display

[](https://diverta.gyazo.com/cecc57b28cfcc1b36d7c29bb37de5b32)

### Field settings

[](https://diverta.gyazo.com/ae3426c39722fa469a73d8353ce6a67e)

Field |  |  | Description
:-- | :-- | :-- | :--
Input type | Required |  | Check this box to make the field mandatory.
Extra columns | Set file extension | Value | Specify the allowed file extension for the upload.
 |  | Add | Add an allowed file extension for the upload.
 |  | Delete | Delete an existing allowed extension.
 | Hide the input field |  | Check this box to hide the file name input field on the content editor screen.
 | Maximum upload size (MB) |  | Limit the size of files that can be uploaded.

### JSON response

```json
details: {
    "ext_col_XX": {
      "id": "sample_0",
      "url": "https://sample.g.kuroco-img.app/v=1623673449/files/topics/sample_0.pdf",
      "dl_link": "https://sample.g.kuroco.app/direct/topics/topics_file_download/?topics_id=960&ext_no=09&index=0",
      "desc": "test"
    },
},
```

## Table

### Content editor display

[](https://diverta.gyazo.com/8377fd13d4ddceec62d9ee6b2cfd865a)

### Field settings

[](https://diverta.gyazo.com/d995c2ca23bc4a129cb9b7bddb044706)

Field |  |  | Description
:-- | :-- | :-- | :--
Input type | Required |  | Check this box to make the field mandatory.
Extra columns | Number of rows |  | Set the number of rows in the table.
 | Number of columns |  | Set the number of columns in the table.
 | Hidden columns |  | Specify any empty columns to be hidden.
 | Cell settings | Cell | Specify the coordinates of the cells. <br>For example, the cell located 2nd from the left and 3 rows down would be `2-3`.
 |  | Value | Enter the value to be displayed in advance when using cell lock.
 |  | Lock | Check this box to lock the cell editing function.
 |  | Punctuation | Check this box to set `<th>` as the cell tag.
 | 　 | Add | Configure the settings for a new cell.
 | 　 | Delete | Delete the settings for the current cell.
 | handsontable |  | Check this box to enable input using Handsontable on the content editor screen.

### JSON response

```json
details: {
    "ext_col_XX": {
      "1": {
        "1": "1-1",
        "2": "1-2",
        "3": "1-3"
      },
      "2": {
        "1": "2-1",
        "2": "2-2",
        "3": "2-3"
      }
    },
},
```

## Location

### Content editor display

[](https://diverta.gyazo.com/40495fbbed2d849b92f9837e0a5e8ad2)

### Field settings

[](https://diverta.gyazo.com/71e86f9d4ecd363847924957ac62a0ed)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.

### JSON response

```json
details: {
    "ext_col_XX": {
      "gmap_x": "139.7435938",
      "gmap_y": "35.7009012",
      "gmap_zoom": "16",
      "gmap_type": "roadmap",
      "gmap_place_id": "ChIJbSFfyl2MGGARIoFxX2bg0hE",
      "jp_lon": "139.0.11.2",
      "jp_lat": "34.59.48.2"
    },
},
```

## TEXT(autocomplete)

### Content editor display

[](https://diverta.gyazo.com/9432099181a86851a062381678a7e19f)

### Field settings

[](https://diverta.gyazo.com/c0766faca87c9407b95c38a866b486e3)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Content structure ID | vvvvvvEnter the group ID of the content to be inputted with autocomplete enabledvvvvvvv.
 | Field | Set the additional field number (e.g., ext_col_04).

### JSON response

```json
details: {
    "ext_col_XX":"Test blog",
},
```

## RelationData Selectbox

### Content editor display

[](https://diverta.gyazo.com/8d2aba82fec2b7d03478fcbdf62ac27f)

### Field settings

[](https://diverta.gyazo.com/68e265128622d33630a20d1922708f6e)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Module | Set the function to be selected as related information.
 | Group ID | If you selected [Content] as the module, specify the ID of the content group designated as related information.
 | Category ID | vvvvvvEnter the group ID of the content to be inputted with autocomplete enabledvvvvvvv.
 | Should have permission to | Specify insert, update, or delete to get the related information that can be executed by the logged-in user.
 | Self only | Check this box to retrieve relevant information created by the logged-in user only.
 | Secure off | Check this box to disable access restrictions.

### JSON response

```json
details: {
    "ext_col_XX": {
        "module_type": "topics",
        "module_id": 959
    },
},
```

## HTML

### Content editor display

[](https://diverta.gyazo.com/a01f17959eef277cda26a30393697fa3)

### Field settings

[](https://diverta.gyazo.com/412e6d205631071794d372c13c565724)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Width | Set the width of the HTML input area.
 | Height | Set the height of the HTML input area.
 | Allow all tags | Check this box to make all tags available.
 | Allow script | Check this box to enable scripts.
 | Smarty | Check this box to enable Smarty.
 | vvvvvvvvvvvvv | Check this box to enable HTML input in the editor.

### JSON response

```json
details: {
    "ext_col_XX":  "<div>\r\nhtml <p>Text area</p>\r\n</div>",
},
```

## Master type

[](https://diverta.gyazo.com/bc558ae2a243ba2b6c3eb54826b38941)

### Content editor display

### Field settings

[](https://diverta.gyazo.com/f41fb554183eca3f5c7ed0974eab5cfe)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Master | Specify the ID of the master to be used.
 | Key | Specify the column number to serve as the key.
 | Value | Specify the column number to serve as the value.
 | Default | Specify the value you want to select during the initial transition.

### JSON response

```json
details: {
    "ext_col_XX": {
        "key": "key",
        "label": "0"
     },
},
```

## File manager

### Content editor display

[](https://diverta.gyazo.com/77b870127534923eb05139cb22371ea3)

### Field settings

[](https://diverta.gyazo.com/af0452bf6ca0202a5ba6f448b0878879)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Specifies the resource | Set the directory path to be displayed upon launching CKFinder.<br> Example: /file/user/

### JSON response

```json
details: {
    "ext_col_XX": false,
},
```

<!--
## APIフィールド

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/c1703cfaeb9f3eff101aa5f9619ca4b3.png?width=600)](https://diverta.gyazo.com/c1703cfaeb9f3eff101aa5f9619ca4b3)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/224f0825c55c2122c614549dc1a52dda.png?width=600)](https://diverta.gyazo.com/224f0825c55c2122c614549dc1a52dda)
|項目 |説明 |
| :--- | :--- |
|必須|チェックを入れると必須入力になります。|
|ポップアップタイトル||
|値復元APIのURL||
|[on_select]ウェブフック||
|[on_save]ウェブフック||
|API settings:Title||
|API settings:URL||
|Add|Collumnを追加します。|
|Delete|Collumnを削除します。|

### JSONレスポンス
```
[APIフィールド]
details: {
    ext_col_XX: false,
},
```
-->

## GCS file

### Content editor display

[](https://diverta.gyazo.com/512365a93081217029551d5485648af9)

### Field settings

[](https://diverta.gyazo.com/f9da9ff33e2e2486c315f8c851654f3c)

Field |  | Description
:-- | :-- | :--
Input type | Required | Check this box to make the field mandatory.
Extra columns | Set file extensions | Specify the allowed file extension for the upload.
 | Add | Add an allowed file extension for the upload.
 | Delete | Delete an existing allowed extension.

<!--
### JSONレスポンス
```[APIフィールド]
details: {
    ext_col_XX: {},
},
```
-->
