# 概要

- WordPress開発チーム公式の開発環境 [wp-env](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/) を使った、WordPress開発環境の雛形。
- テーマ開発、プラグイン開発に特化。
- 必須プラグインやテーマを、[.wp-env.jsonで予め設定](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/#wp-envjson)できて効率的。
- .wp-env.json は都度ブラッシュアップする。

## 前提

1. [Docker Desktop](https://www.docker.com/) セットアップ済。
2. [Node.js](https://nodejs.org/ja/) セットアップ済。
3. __node バージョンはLTS推奨なので確認しておく。__

- nodeはVoltaで管理しているのでコマンドは以下。
- 使い方記事 👉 [Qiita](https://qiita.com/25master/items/7e03ef3745656c98d5ee#%E4%BD%BF%E3%81%84%E6%96%B9)

```bash
# Volta 管理下の各種バージョンを確認するのに使用
volta list

# Volta で管理しているツールを一覧で見る
volta list all
```

4. 開発ディレクトリを作成し、移動する。
   1. `mkdir hoge`
   2. `cd hoge`

## 手順

1. `npm i -D @wordpress/env`
2. ~~`npm init -y`~~
   ~~1.  package.json生成~~
3. package.json の `scripts` に `wp-env` コマンドを追記。**※記載箇所注意**
4. [.wp-env.json](https://github.com/chum9625/wp-env-model/blob/main/.wp-env.json) を作成。
5. 起動 `npm run wp-env start`

   | 動作   | コマンド                      |
   | ------ | ----------------------------- |
   | 起動   | npm run wp-env start          |
   | 停止   | npm run wp-env stop           |
   | 再起動 | npm run wp-env start --update |
   | 削除   | npm run wp-env destroy        |

6. トップページ表示確認 http://localhost:8888
7. 管理画面ログイン http://localhost:8888/wp-login.php

   | ユーザー名 | パスワード |
   | ---------- | ---------- |
   | admin      | password   |

## DBへの接続

- 起動コマンドを実行後 `docker ps` でDBのポートをコピーする。
- 接続情報

   | パラメータ | 値             |
   | ---------- | -------------- |
   | Host       | 0.0.0.0        |
   | Port       | コピーした番号 |
   | User       | root           |
   | Password   | password       |
   | Database   | wordpress      |

## トラブルシューティング

- [一般的な問題のトラブルシューティング](https://ja.wordpress.org/team/handbook/block-editor/reference-guides/packages/packages-env/#%E4%B8%80%E8%88%AC%E7%9A%84%E3%81%AA%E5%95%8F%E9%A1%8C%E3%81%AE%E3%83%88%E3%83%A9%E3%83%96%E3%83%AB%E3%82%B7%E3%83%A5%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0)

---

### 付録1. SSHでサーバーにWordPressをインストールする

1. 本番サーバーにSSHで接続する。
2. インストールするディレクトリに移動。 `cd /web/public_html/hoge`
3. WordPress最新版をダウンロード。 `wget http://ja.wordpress.org/latest-ja.tar.gz`
4. 解凍。（/wordpress/に解凍される） `tar -zxvf latest-ja.tar.gz`
5. 配置したいディレクトリにファイルを移動する。例）  `mv ./wordpress/* ./`
6. 不要なディレクトリ、ファイルを削除。 例） `rm -r latest-ja.tar.gz wordpress`

### 付録2. 開発用空テーマ _s を使う

1. [underscores.me](https://underscores.me/) で、空テーマを取得する。
   1. sassを使う場合、 *Advanced Options* をクリックし、 ✅ sassify!にチェックを入れる。
2. __my-theme__ という名前のテーマを作成したい場合、 __my-theme__ と入力してGENERATEボタンをクリック（ダウンロード）する。
3. ダウンロードしたものをテーマのスターターとして使う。

### 付録3. WordPress REST API の準備

1. 初期状態で叩いてもNot　Found　となる ``` http://localhost:8888/wp-json/wp/v2/posts ```
2. REST API を利用するためには、設定 ＞ パーマリンク から　「投稿名」　を選択して　「変更を保存」　する必要がある
