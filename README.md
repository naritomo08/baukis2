# Baukis2 - 顧客管理システム

## 説明

Baukis2 は企業向けの顧客管理システム（Ruby on Rails 学習用サンプル）です。

## 推奨されるシステム環境

* Ubuntu 18.04
* Ruby 2.6.4
* PostgreSQL 11.2

## 注意事項

* 以下の手順では、一般ユーザーの権限でコマンドを実行してください。

## インストール手順

* この `README.md` が存在するディレクトリで `bin/bundle` コマンドを実行してください。

## データベースのセットアップ

* このシステム専用のデータベースを PostgreSQL 上に作成してください。
* データベースへの接続パラメータに基づいて `config/database.yml` を作成してください。
* `bin/rails db:setup` コマンドを実行してください。

## hosts ファイルの設定

* ホスト OS の `hosts` ファイルに次の 1 行を追加してください（要 root 権限）。
  `hosts` ファイルは、Mac OS X の場合は `/private/etc/hosts` フォルダに、
  Windows の場合は `C:\Windows\system32\drivers` フォルダにあります。

      127.0.0.1 example.com baukis2.example.com

## システムの起動と終了

* `rails s -b 0.0.0.0` コマンドを実行するとシステムが起動します。
* Ctrl-C を入力するとシステムが終了します。

## システムの利用

* ブラウザで以下の URL にアクセスしてください:
  * http://baukis2.example.com:3000 -- 職員向けサイト
  * http://baukis2.example.com:3000/admin -- 管理者向けサイト
  * http://example.com:3000/mypage -- 顧客向けサイト


# 補足事項

## アカウント
```
顧客
ito.ichiro@example.jp
password

職員
taro@example.com
password

管理者
hanako@example.com
foobar
```

## apサーバログイン
```
docker-compose exec web bash
cd baukis2
```

## webサービス立ち上げ(開発モード)
```
rails s -b 0.0.0.0
```

## プリコンパイル(本番環境反映)
```
bin/rails db:reset RAILS_ENV=production
bin/rails assets:precompile RAILS_ENV=production
```

## 本番環境マスターキー確認
```
EDITOR=vim bin/rails credentials:edit

エラーが出る場合
rm config/credentials.yml.enc config/master.key
EDITOR=vim bin/rails credentials:edit
```

## webサービス立ち上げ(本番モード)
```
export RAILS_SERVE_STATIC_FILES=1
rails s -e production -b 0.0.0.0
```

## サービス立ち上げ時、"warning Integrity check: Flags don't match"が出る場合
```
yarn upgrade
```

## サービス立ち上げ時、"Could not find *** in any of the sources”が出る場合
```
bundle install
```

## dbコマンド

```
rails db:setup
rails db:migrate
rails db:migrate:reset
rails db:seed
rails db:reset
```

## 初回のシステム立ち上げ方

```
dockerをあらかじめ立ち上げていて、dockerフォルダにいること。
cd apps
git clone -b book2-naritomo-kansei git@github.com:naritomo08/baukis2.git
docker-compose exec web bash
cd baukis2
bundle install
yarn
rails db:reset
rails s -b 0.0.0.0
サイト表示ができていることを確認する。
```

# 本番データ投入

```
adminerを使用して、
baukis_production/administratorテーブルに対し、以下のデータを入れる。

email:hanako@example.com
hashed_passsword:$2a$12$PSYJCyRhFsJ6hAu/q1LXh.u3Neq3Zi6LGiO7KF4qwA9IoGlz7.VDC
created_at:now
updated_at:now

管理者画面にログインできることを確認する。
```