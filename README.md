# wp-env-model

- WordPress開発チーム公式の開発環境 [wp-env](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/) を使った、WordPress開発環境の雛形。
- 開発環境で使用するプラグインやテーマを、[.wp-env.json](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/#wp-envjson)で予め設定できるので便利。
- このリポジトリはcloneではなくjsonファイルを参照し活用する。

## 前提

1. [Docker Desktop](https://www.docker.com/) セットアップ済。
2. [Node.js](https://nodejs.org/ja/) セットアップ済。
3. テーマディレクトリを作成し、移動しておく。
   1. `mkdir my-theme`
   2. `cd my-theme`
4. __node バージョンはLTS推奨。__
   1. バージョン確認 ` nvm ls `
   2. バージョン変更 ` nvm use [version number] `
   3. [Node.jsインストール方法](https://qiita.com/ffggss/items/94f1c4c5d311db2ec71a#nodejs%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)

## 手順

1. `npm i -D @wordpress/env`
2. ~~`npm init -y`~~
   ~~1.  package.json生成~~
3. package.json の `scripts` に `wp-env` コマンドを追記。**※記載箇所注意**
4. `.wp-env.json` を作成。　**※プラグイン見直し　特にewww**
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

## トラブルシューティング

- [一般的な問題のトラブルシューティング](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/#%E4%B8%80%E8%88%AC%E7%9A%84%E3%81%AA%E5%95%8F%E9%A1%8C%E3%81%AE%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)
