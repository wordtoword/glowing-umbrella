---
title: List of additional fields available in the content structure
category: Content
weight: 1
---

By default, the content editor contains the following 3 fields: 
- Topic ID/Slug
- Date
- Title

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/58ffd2e6c2f2cc9ae7026d9f72ea8b65.png)](https://diverta.gyazo.com/58ffd2e6c2f2cc9ae7026d9f72ea8b65)

You can set up additional fields using the content structure editor.

See [Content structure - Extended items](/docs/management/content-structure-topics-group/#extended-items) for a detailed guide.

[![Image from Gyazo](https://t.gyazo.com/teams/diverta/4d054a9b6a1b59344039b26dd344fd79.png)](https://diverta.gyazo.com/4d054a9b6a1b59344039b26dd344fd79)

Extended items can also be configured by clicking on "Settings" to open the settings screen, where you can set input restrictions and the content to be displayed.
また、拡張項目は[設定]をクリックして設定画面を開くと、入力制限や表示させる内容を設定することができます。  

[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/d33a6204935c6041db2b78ec42b8f7d5.png?width=600)](https://diverta.gyazo.com/d33a6204935c6041db2b78ec42b8f7d5)

設定できる内容は項目により異なりますので下記参照ください。

## 拡張項目一覧
[テキスト](#テキスト)  
[テキストエリア](#テキストエリア)  
[選択形式](#選択形式)  
[画像](#画像)  
[複数選択(チェックボックス)](#複数選択チェックボックス)  
[Wysiwyg](#wysiwyg)  
[リンク](#リンク)  
[日付フォーマット](#日付フォーマット)  
[ファイル](#ファイル)  
[表組(テーブル)](#表組テーブル)  
[地図](#地図)  
[テキスト(オートコンプリート)](#テキストオートコンプリート)  
[関連情報選択](#関連情報選択)  
[html](#html)  
[マスタ形式](#マスタ形式)  
[ファイルマネージャ](#ファイルマネージャ)  
[GCS上のファイル](#gcs上のファイル) 
<!--[APIフィールド](#apiフィールド)-->

## テキスト
### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/2b020827382500d55c16b1e0340edf88.png?width=600)](https://diverta.gyazo.com/2b020827382500d55c16b1e0340edf88)
### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/ba1392b10c24f23116f559b4441e59ff.png?width=600)](https://diverta.gyazo.com/ba1392b10c24f23116f559b4441e59ff)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
| |入力制限|入力できる文字列を制限することができます。|
| |正規表現|入力制限で[正規表現]を選択した場合は正規表現を記入します。|
| |文字数制限|最小・最大の文字数を設定します。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": "テキスト",
},
```

## テキストエリア
### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/d0e13478b3325c54a3d07f862477a42c.png?width=600)](https://diverta.gyazo.com/d0e13478b3325c54a3d07f862477a42c)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/c0f0b14dbece2871d3544338eb4f1d8c.png?width=600)](https://diverta.gyazo.com/c0f0b14dbece2871d3544338eb4f1d8c)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|横幅|表示するテキストエリアの横幅を設定します。|
| |縦幅|表示するテキストエリアの縦幅を設定します。|
| |文字数制限|最小・最大の文字数を設定します。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": "テキストエリア",
},
```

## 選択形式
### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/43185a1a7a2dd1e1c147cb617117c434.png?width=600)](https://diverta.gyazo.com/43185a1a7a2dd1e1c147cb617117c434)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/d4d92f19fc697c4a1525da09a8826f27.png?width=600)](https://diverta.gyazo.com/d4d92f19fc697c4a1525da09a8826f27)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力項目|必須|チェックを入れると必須入力になります。|
|選択項目|key|選択項目のKeyを記入します。|
|　|Value|選択項目のValueを記入します。|
|　|デフォルト|チェックを入れると対象の項目がデフォルトで選択された状態になります。|
|　|Add|選択項目を追加します。|
|　|Delete|選択項目を削除します。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": { 
        "key": "1",
        "label": "選択肢1" 
    },
},
```

## 画像

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/94114d049036d27837cfc29231591460.png?width=600)](https://diverta.gyazo.com/94114d049036d27837cfc29231591460)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/c5b39a446ba8766eaa74e04184035116.png?width=600)](https://diverta.gyazo.com/c5b39a446ba8766eaa74e04184035116)

|項目 | | |説明 |
| :--- | :--- | :--- | :--- |
|入力関連|必須| |チェックを入れると必須入力になります。|
|拡張項目|拡張子 |Value|アップロードを許可する画像の拡張子を指定します。|
| | |Add|アップロードを許可する画像の拡張子を追加します。|
| | |Delete|アップロードを許可する画像の拡張子を削除します。|
| |最大アップロードファイルサイズ(MB)| |アップロード可能な画像のサイズに制限をかけます。|
| |キャプション入力欄を非表示| |チェックを入れると、コンテンツ編集画面で画像の説明の入力欄を非表示にします。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": {
        "id": "sample_0",
        "url": "https://sample.g.kuroco-img.app/v=1623673449/files/topics/sample.png",
        "desc": ""
    },
},
```

## 複数選択(チェックボックス)
### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/ffdc4592f837335b553e0c0d45635019.png?width=600)](https://diverta.gyazo.com/ffdc4592f837335b553e0c0d45635019)
### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/b803ae32fe2918e922fcf988b0950b2c.png?width=600)](https://diverta.gyazo.com/b803ae32fe2918e922fcf988b0950b2c)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|選択項目|key|選択項目のKeyを記入します。|
| |Value|選択項目のValueを記入します。|
| |デフォルト|チェックを入れると対象の項目がデフォルトで選択された状態になります。|
| |Add|選択項目を追加します。|
| |Delete|選択項目を削除します。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": [
        {
            "key": "1",
            "label": "複数選択_選択肢1"
        },
        {
            "key": "2",
            "label": "複数選択_選択肢2"
        }
    ],
},
```

## Wysiwyg

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/ef63db8198ad3b1123ba0724c0866d39.png?width=600)](https://diverta.gyazo.com/ef63db8198ad3b1123ba0724c0866d39)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/313957be252c65b85760fa0e218a2c3f.png?width=600)](https://diverta.gyazo.com/313957be252c65b85760fa0e218a2c3f)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|色指定|色の変更ができます。|
| |横幅|フィールドの横幅を指定します。|
| |縦幅|フィールドの縦幅を指定します。|
| |削除するプラグイン|不要なブラグインを記入します。|
| |シンプルなツールバー|チェックを入れると、シンプルなツールバーになります。|

### JSONレスポンス
```json
"details": {
    "ext_col_XX": "<p><strong>Wysiwyg</strong> テキストエリア</p>",
},
```

## リンク

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/336378da627557b9e1c021a7e11ae599.png?width=600)](https://diverta.gyazo.com/336378da627557b9e1c021a7e11ae599)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/27cdf0a0a874f8dd63e8738f3e2f6a04.png?width=600)](https://diverta.gyazo.com/27cdf0a0a874f8dd63e8738f3e2f6a04)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": { 
        "url": "https://kuroco.app/",
        "title": "Kuroco"
    },
},
```

## 日付フォーマット

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/38836415f185cdded83424f406f3466a.png?width=600)](https://diverta.gyazo.com/38836415f185cdded83424f406f3466a)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/2633ef674ed074922102f7593a0d95ec.png?width=600)](https://diverta.gyazo.com/2633ef674ed074922102f7593a0d95ec)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|時間も設定する|チェックを入れると時間の設定ができるようになります。|

### JSONレスポンス
```json
details: {
    "ext_col_XX":"2021-06-04",
},
```

## ファイル

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/cecc57b28cfcc1b36d7c29bb37de5b32.png?width=600)](https://diverta.gyazo.com/cecc57b28cfcc1b36d7c29bb37de5b32)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/ae3426c39722fa469a73d8353ce6a67e.png?width=600)](https://diverta.gyazo.com/ae3426c39722fa469a73d8353ce6a67e)

|項目 | | |説明 |
| :--- | :--- | :--- | :--- |
|入力関連|必須| |チェックを入れると必須入力になります。|
|拡張項目|拡張子の設定|Value|アップロードを許可するファイルの拡張子を指定します。|
| | |Add|アップロードを許可するファイルの拡張子を追加します。|
| | |Delete|アップロードを許可するファイルの拡張子を削除します。|
| |入力欄を非表示| |チェックを入れると、コンテンツ編集画面でファイル名の入力欄を非表示にします。|
| |最大アップロードファイルサイズ(MB)| |アップロード可能なファイルのサイズに制限をかけます。|

### JSONレスポンス
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

## 表組(テーブル)

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/8377fd13d4ddceec62d9ee6b2cfd865a.png?width=600)](https://diverta.gyazo.com/8377fd13d4ddceec62d9ee6b2cfd865a)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/d995c2ca23bc4a129cb9b7bddb044706.png?width=600)](https://diverta.gyazo.com/d995c2ca23bc4a129cb9b7bddb044706)

|項目 | | |説明 |
| :--- | :--- | :--- | :--- |
|入力関連|必須| | チェックを入れると必須入力になります。|
|拡張項目|行の数| |テーブルの行の数を指定します。|
| |列の数| |テーブルの列の数を指定します。|
| |非表示の列| |テーブル内に入力がない場合、非表示にする列を指定します。|
| |セルの設定|セル|設定を行うセルを指定します。<br/>上から2行目、左から3列目のセルを指定する場合は`2-3`と記述します。|
| | |値|セルをLOCKする場合に、予め表示する値を記入します。|
| | |LOCK|チェックを入れるとセルの編集をLOCKします。|
| | |区切り|チェックを入れるとセルのタグが`<th>`になります。|
| |　|Add|セルの設定を追加します。|
| |　|Delete|セルの設定を削除します。|
| |handsontable| |チェックを入れるとコンテンツ編集画面でhandsontable を利用した入力ができるようになります。|

### JSONレスポンス
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

## 地図

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/40495fbbed2d849b92f9837e0a5e8ad2.png?width=600)](https://diverta.gyazo.com/40495fbbed2d849b92f9837e0a5e8ad2)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/71e86f9d4ecd363847924957ac62a0ed.png?width=600)](https://diverta.gyazo.com/71e86f9d4ecd363847924957ac62a0ed)

|項目| |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|

### JSONレスポンス
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

## テキスト(オートコンプリート)

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/9432099181a86851a062381678a7e19f.png?width=600)](https://diverta.gyazo.com/9432099181a86851a062381678a7e19f)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/c0766faca87c9407b95c38a866b486e3.png?width=600)](https://diverta.gyazo.com/c0766faca87c9407b95c38a866b486e3)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|コンテンツ定義ID|オートコンプリート表示するコンテンツ定義グループIDを設定します|
| |Field|オートコンプリート表示する拡張番号を設定します <br/>例:ext_col_04|

### JSONレスポンス
```json
details: {
    "ext_col_XX":"テストブログ",
},
```

## 関連情報選択

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/8d2aba82fec2b7d03478fcbdf62ac27f.png?width=600)](https://diverta.gyazo.com/8d2aba82fec2b7d03478fcbdf62ac27f)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/68e265128622d33630a20d1922708f6e.png?width=600)](https://diverta.gyazo.com/68e265128622d33630a20d1922708f6e)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|モジュール|関連情報として選択させる機能を指定します。|
| |グループID|モジュールをコンテンツに設定した場合に、関連情報として選択させるグループのIDを指定します。|
| |カテゴリID|モジュールをコンテンツに設定した場合に、関連情報として選択させるカテゴリのIDを指定します。|
| |Should have permission to|insert,update,deleteを指定して、そのうちログインしているユーザーが実行できる関連情報が取得されます。|
| |Self only|ログインしているユーザーが作成した関連情報だけが取得されます。|
| |Secure off|閲覧制限を無効にして関連情報取得可能になります。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": {
        "module_type": "topics",
        "module_id": 959
    },
},
```

## html

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/a01f17959eef277cda26a30393697fa3.png?width=600)](https://diverta.gyazo.com/a01f17959eef277cda26a30393697fa3)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/412e6d205631071794d372c13c565724.png?width=600)](https://diverta.gyazo.com/412e6d205631071794d372c13c565724)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|横幅|表示するhtml入力エリアの横幅を設定します。|
| |縦幅|表示するhtml入力エリアの縦幅を設定します。|
| |全てのタグを許可する|チェックを入れると全てのタグが利用可能になります。|
| |scriptを許可|チェックを入れるとscriptが利用可能になります。|
| |Smarty|チェックを入れるとSmartyが利用可能になります。|
| |エディタを使う|チェックを入れるとhtmlの入力がエディタ利用になります。|

### JSONレスポンス
```json
details: {
    "ext_col_XX":  "<div>\r\nhtml <p>テキストエリア</p>\r\n</div>",
},
```

## マスタ形式
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/bc558ae2a243ba2b6c3eb54826b38941.png?width=600)](https://diverta.gyazo.com/bc558ae2a243ba2b6c3eb54826b38941)
### コンテンツ編集画面の表示
### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/f41fb554183eca3f5c7ed0974eab5cfe.png?width=600)](https://diverta.gyazo.com/f41fb554183eca3f5c7ed0974eab5cfe)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|マスタ|利用するマスタのIDの指定します。|
| |キー|キーとして使用する列番号を指定します。|
| |値|値として使用する列番号を指定します。|
| |デフォルト|初期遷移時に選択済みにしたい値を指定します。|

### JSONレスポンス
```json
details: {
    "ext_col_XX": { 
        "key": "key",
        "label": "0"
     },
},
```

## ファイルマネージャ

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/77b870127534923eb05139cb22371ea3.png?width=600)](https://diverta.gyazo.com/77b870127534923eb05139cb22371ea3)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/af0452bf6ca0202a5ba6f448b0878879.png?width=600)](https://diverta.gyazo.com/af0452bf6ca0202a5ba6f448b0878879)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|リソースを指定|ckfinder起動時に表示したいディレクトリパス指定します。<br/>例: /file/user/

### JSONレスポンス
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

## GCS上のファイル

### コンテンツ編集画面の表示
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/512365a93081217029551d5485648af9.png?width=600)](https://diverta.gyazo.com/512365a93081217029551d5485648af9)

### 項目設定
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/f9da9ff33e2e2486c315f8c851654f3c.png?width=600)](https://diverta.gyazo.com/f9da9ff33e2e2486c315f8c851654f3c)

|項目 | |説明 |
| :--- | :--- | :--- |
|入力関連|必須|チェックを入れると必須入力になります。|
|拡張項目|Value|アップロードを許可するファイルの拡張子を指定します。|
| |Add|拡張子の設定を追加します。|
| |Delete|拡張子の設定を削除します。|

<!--
### JSONレスポンス
```[APIフィールド]
details: {
    ext_col_XX: {},
},
```
-->
