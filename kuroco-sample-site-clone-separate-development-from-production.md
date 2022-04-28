---
title: 会員制サンプルサイトで、開発環境と本番環境を分ける方法
description: 開発環境と本番環境を分ける対応方法を学べます。開発環境と本番環境を分けることにより、変更や修正があった場合に本番サイトへの変更を公開する前に確認できます。
---

本チュートリアルでは、開発環境と本番環境を分ける対応方法を学べます。  
開発環境と本番環境を分けることにより、変更や修正があった場合に本番サイトへの変更を公開する前に確認できます。

## 前提条件
本チュートリアルは、オープンソースで公開している[会員制サンプルサイト](https://github.com/diverta/front_nuxt_auth)(NuxtAuthベースのKurocoFrontテンプレートサイト)をコピーしてサイトを構築をしていることが必要となります。  
まだサイト構築していない場合は、[会員制サンプルサイトをコピーして、Kurocoで会員制サイトを構築する方法](/ja/docs/tutorials/kuroco-sample-site-clone/)を参考に構築をお願いします。

## 概要

今回、下記2種類の環境を用意することを前提とします。

- 開発環境
- 本番環境

開発する際の確認順序として、開発環境 -> 本番環境と段階的に確認/公開していく手順を想定しています。

GitHubにはそれぞれの環境に対応するブランチを作成し、それぞれのブランチが変更される度にGitHub Actionsが動作します。
また、自動でその対応する環境のフロントエンドが変更されるフローを設定していきます。

## 独自ドメインの設定

[KurocoFrontで独自ドメインを利用する手順](/ja/docs/tutorials/how-to-use-original-domain-on-kuroco-front/)を参考に独自ドメインを設定してください。

また、今回は`フロントドメイン`と`APIドメイン`はサブドメイン関係(ドメインが一致する/ファーストパーティcookieとなる状態)に変更してください。
会員制サンプルサイトが利用しているCookieログイン方式においては、サードパーティcookie制限によりブラウザ/利用環境によってはcookieを維持できない可能性があるためです。

参考:[セキュリティ設定：Cookie で記事データを表示する](/ja/docs/tutorials/how-to-use-swagger-ui/#セキュリティ設定：cookie-で記事データを表示する)

## GitHubの設定

今回GitHubのリポジトリを上記2つのブランチに分ける必要があります。
下記のようにブランチを作成してください。

|項目   |ブランチ  |
| :--- | :--- |
| 本番環境 | main |
| 開発環境 | develop |

[[info]]
ブランチの分け方は、[GitHub公式ドキュメント](https://docs.github.com/ja/desktop/contributing-and-collaborating-using-github-desktop/making-changes-in-a-branch/managing-branches)を参照してください。  

[[info]]
想定外の本番環境への公開を防ぐために、mainブランチにはプロテクションをかけることをお勧めします。ブランチの保護の方法は、[GitHub公式ドキュメント](https://docs.github.com/ja/github/administering-a-repository/defining-the-mergeability-of-pull-requests/managing-a-branch-protection-rule)を参照してください。

## GitHubActions用Buildファイルの修正

既存の`/.github/workflow/build.yml`を修正し、develop/mainブランチでそれぞれ想定した動作をするように修正します。

下記を修正します。
- [develop/main用のbuild定義を作成する](#developmain用のbuild定義を作成する)
- [Buildファイルのイベントを変更する](#buildファイルのイベントを変更する)
- [ビルドとデプロイ先をそれぞれの環境用へ設定する](#ビルドとデプロイ先をそれぞれの環境用へ設定する)
- [(存在する場合)開発用kuroco_front.jsonの適用](#存在する場合開発用kuroco_frontjsonの適用)


### develop/main用のbuild定義を作成する
本番環境と開発環境用に２つのbuildファイルを作成します。  
今回は下記のファイルを作成します。

- 本番環境用: `.github/workflows/build.yml`
- 開発環境用: `.github/workflows/develop.yml`

`.github/workflows/build.yml`はすでに存在するので、こちらをコピーし`.github/workflows/develop.yml`を作成してください。

### Buildファイルのイベントを変更する
次に各Buildファイルを修正します。
下記のように、それぞれのブランチが変更された時にだけイベントが発生するようにします。

- 本番環境：mainブランチが変更された時にのみイベント発生
- 開発環境：developブランチが変更された時のみイベント発生

今回は開発環境用の`.github/workflows/develop.yml`を下記のように修正します。

```YAML [.github/workflows/develop.yml]
 on:
   push:
     branches:
      - develop
   workflow_dispatch:
    branches: [ develop ]
 jobs:
   build:
     name: Build
```

### ビルドとデプロイ先をそれぞれの環境用へ設定する
それぞれの環境に適したビルドを行うような動作へ変更修正します。

今回は下記のnpm scriptが動作するように修正します。
- 本番環境用は`build-prod`および`generate-prod`
- 開発環境用は`build`および`generate`

今回は本番環境用の`.github/workflows/build.yml`を下記のように修正します。

```YAML [.github/workflows/build.yml]
       - name: Install dependencies
         run: npm ci
       - name: Build
         run: npm run build-prod
       - name: Generate
         run: npm run generate-prod
       - name: Archive Production Artifact
         uses: actions/upload-artifact@v2
         with:
```

### 開発環境用のkuroco_front.jsonを作成する
次に、開発環境用にkuroco_front.jsonを作成します。
`/src/static` 配下の`kuroco_front.json`をコピーして、`kuroco_front_dev.json`を作成します。

[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/26518d6b65f37f5cf5c4be2b925cd165.png?width=600)](https://diverta.gyazo.com/26518d6b65f37f5cf5c4be2b925cd165)

また、`develop.yml`のみに`kuroco_front_dev.json`を適用する必要があります。`develop.yml`に下記を追記します。

```diff
     steps:
       - name: Checkout Repo
         uses: actions/checkout@v2
+      - name: Copy kuroco_front.json
+        run:  cp src/static/kuroco_front_dev.json src/static/kuroco_front.json 
       - name: Use Node.js
         uses: actions/setup-node@v1
         with:
```

参考: kuroco_front.jsonについては、[kuroco_front.jsonとは何ですか？](/ja/docs/faq/what-is-kuroco_front_json/)をご確認ください。

## npm scriptの確認
次に、npm scriptを確認します。npm scriptとはNode.jsが実行する簡易コマンドです。  
上述した`build-prod`や`build`コマンドはこのnpm scriptを実行している箇所で、
NuxtAuthにおいては、package.jsonにあらかじめその内容が記載されています。

package.jsonを抜粋すると、下記のように設定されています。
```json [package.json]
{
  ...,
  "scripts": {
    ...
    "build": "cross-env NODE_ENV=development nuxt build",
    "generate": "cross-env NODE_ENV=development nuxt generate",
    "build-prod": "cross-env NODE_ENV=production nuxt build",
    "generate-prod": "cross-env NODE_ENV=production nuxt generate",
    ...
  },
  ...
}
```
現在`build`と`build-proud`では`NODE_ENV=...`の値が異なっています。
- build: NODE_ENV=development nuxt build
- build-prod: NODE_ENV=production nuxt build

ここの値はnuxtをビルドするときの設定ファイルである`nuxt.config.js`に影響してます。

`nuxt.config.js`を確認すると、下記のように記載があります。

```js
const environment = process.env.NODE_ENV; // <- (※1)
const envSettings = require(`./env.${environment}.js`); 

export default {
    env: envSettings,
    
    ...

    head: {
        htmlAttrs: {
            lang: 'ja'
        },
        titleTemplate: '%s - ',
        title: envSettings.META_TITLE,  // <- (※2)
...
```

(※1)の箇所で、上述していた`NODE_ENV=...`が指定されるので、npm scriptの違いで下記のように、動的に変更されます。
- `build` の場合は `require('./env.develop.js')`
- `build-prod` の場合は `require('./env.production.js')`

例えば(※2)のMETAタイトルの値が、それぞれの`env.${environment}.js`ファイルから設定される仕組みになっています。

## envファイルの確認・修正
それでは現在のenvファイルの確認・修正します。  
開発環境/本番環境の`./env.${environment}.js`ファイルは下記のようにすでに存在しています。
- `env.development.js`
- `env.production.js`

これを作成したKurocoの環境ごとに変更します。
今回は下記のように修正しました。

```js [env.production.js]
module.exports = {
    META_TITLE: 'Nuxt Auth',
    ROBOTS: 'index',
    BASE_URL: 'https://[独自APIドメイン]'
};
```

```js [env.development.js]
module.exports = {
    META_TITLE: '[開発] Nuxt Auth',
    ROBOTS: 'noindex',
    BASE_URL: 'https://[独自APIドメイン]'
};
```
注: 独自APIドメインは、[独自ドメインの設定](#独自ドメインの設定)で設定した内容を記載してください。

このように変更することで、下記が動的に変更されます。
- 本番環境のMETA TITLE：Nuxt Auth
- 開発環境のMETA TITLE: [開発] Nuxt Auth

以上で本番環境と開発環境の設定完了です。

## 動作確認
それでは、ここまで設定した内容を確認します。今回は開発環境のみを確認します。

まずは、developブランチをリモートリポジトリにpushします。  
push後、GitHubの当該リポジトリにアクセスし、「Actions」をクリックします。
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/247b06ff22179debabff76c01f2cb753.png?width=600)](https://diverta.gyazo.com/247b06ff22179debabff76c01f2cb753)

動作中/動作終了したActions一覧が表示されます。
[![Image (fetched from Gyazo)](https://rcms.g.kuroco-img.app/files/user/gyazo/71c92f92e53e12f2a049c11055a57f7a.png?width=600)](https://diverta.gyazo.com/71c92f92e53e12f2a049c11055a57f7a)

ビルドが完了後、開発環境のMETA TITLEを確認いただくと、**[開発] Nuxt Auth** と表示されていることが確認できます。

以上で確認完了です。
