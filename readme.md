<div id="top"></div>

## 使用技術一覧

<p style="display: inline">
    <p>docker</p>
    <p>nginx</p>
    <p>mkcert</p>
</p>


## 目次

- [使用技術一覧](#使用技術一覧)
- [目次](#目次)
- [プロジェクト名](#プロジェクト名)
- [プロジェクトについて](#プロジェクトについて)
- [環境](#環境)
- [ディレクトリ構成](#ディレクトリ構成)
- [設定について](#設定について)
- [開発環境構築](#開発環境構築)
  - [ssl-keyの作成](#ssl-keyの作成)
  - [実行](#実行)
- [トラブルシューティング](#トラブルシューティング)
  - [全般](#全般)
  - [ブラウザ開くと警告が..](#ブラウザ開くと警告が)


## プロジェクト名

ローカルでhttps通信によるフロントエンドの動作確認するためのプロキシ


## プロジェクトについて

ローカルでhttps通信によるフロントエンドの動作確認するためのプロキシ


## 環境

| 言語・フレームワーク  | バージョン |
| --------------------- | ---------- 
| docker                | 3.8
| nginx                 | 1.21-alpine
| mkcert                | 1.4.4


## ディレクトリ構成

├── docker-compose.yml
├── nginx
│   ├── Dockerfile
│   ├── conf.d
│   │   └── default.conf
│   ├── log
│   │   ├── access.log
│   │   └── error.log
│   └── ssl
│       ├── localhost-key.pem
│       └── localhost.pem
└── readme.md

## 設定について
* nginxの設定
  * nginx/conf.d/default.conf
  * upstream frontend の内容を起動するfrontendサイトのものに修正する
    * 設定を行うことでfrontendサイトに https://localhost:20443 (docker-compose.yamlで指定したポート) でアクセスすることが可能
* docker-compose.yaml
  * portsの内容を変更するとfrontendサイトに何番ポートでアクセスするか指定できる
  * 初期はひとまず `127.0.0.1:20443:443` にしてある
    * 127.0.0.1:20443 でアクセスすると 443 ポート(httpsの うえるのうん番号)でアクセスしたことになります

## 開発環境構築
mac環境を想定しているのでwindows環境で試していません..（ごめんなさい..）

### ssl-keyの作成
* 現状mkcert を使用しています (参考:https://entreprogrammer.jp/ssl-mkcert/)
* mkcert を install
* `mkcert -install`
    * 二進も三進もいかない時は`mkcert -uninstall`も良いのかも
* `mkcert localhost`
* できた二つのファイル（証明書と秘密鍵）をsslフォルダに
    * conf.d/default.conf にsshの設定が書かれてる
* simulatorにインストールが必要なら、鍵をエクスポート(書き出し)後、ドラッグ&ドロップで
    * キーチェーン(MAC)などで確認できる

### 実行
* dockerを起動しておく
* `docker compose up -d` を実行
    * `-d` を入れるとコンテナの外にでた状態で実行できる
* 終わる時は `docker compose down`


## トラブルシューティング
### 全般
* とりあえずlogフォルダに access.log, error.log があるのでまずはそこをみる..


### ブラウザ開くと警告が..
* ssl-key が切れているかも..再作成が必要？
    * 現状mkcert を使用しています (参考:https://entreprogrammer.jp/ssl-mkcert/)
    * mkcert を install
    * `mkcert -install`
        * 二進も三進もいかない時は`mkcert -uninstall`も良いのかも
    * `mkcert localhost`
    * できた二つのファイル（証明書と秘密鍵）をsslフォルダに
        * conf.d/default.conf にsshの設定が書かれてる
    * simulatorにインストールが必要なら、鍵をエクスポート(書き出し)後、ドラッグ&ドロップで
        * キーチェーン(MAC)などで確認できる

