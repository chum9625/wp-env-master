# wp-env-model

- WordPress開発チーム公式の開発環境 [wp-env](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/) を使ったオリジナル環境。

## 前提

1. [Docker Desktop](https://www.docker.com/) セットアップ済。
2. [Node.js](https://nodejs.org/ja/) セットアップ済。
3. テーマディレクトリを作成し、移動。
   1. mkdir my-theme
   2. cd my-theme

## 手順

1. `npm i -D @wordpress/env`
2. `npm init -y`
   1.  package.json生成
3. package.json の `scripts` に `wp-env` コマンドを追記。
4. .wp-env.json を作成。
5. 起動 `npm run wp-env start`
   1. 停止   `npm run wp-env stop`
   2. 再起動 `npm run wp-env start --update`
   3. 削除   `npm run wp-env destroy`
6. トップページ http://localhost:8888
7. 管理画面 http://localhost:8888/wp-login.php
   1. `admin`
   2. `password`

## DBへの接続

- 起動コマンドを実行後 `docker ps` でDBのポートをコピーする。
- 接続情報

|パラメータ|値|
|----|----|
|Host|0.0.0.0|
|Port| コピーした番号|
|User|root|
|Password|password|
|Database|wordpress|
