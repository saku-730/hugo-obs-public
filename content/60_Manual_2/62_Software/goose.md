---
title: goose
tags:
  - 2025/12
  - Go
created: 2025-12-18
updated: 2026-04-26
draft: false
---
## install

```bash
go install github.com/pressly/goose/v3/cmd/goose@latest
```

go 1.21以上のインストールが必要。

パスを通す

```bash
export PATH="$(go env GOPATH)/bin:$PATH"
hash -r
which goose
goose -version
```

```bash
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.bashrc
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.profile

source ~/.bashrc
which goose
goose -version
```

## 設定

環境変数を設定する必要がある。(一応毎回、コマンドにつければ環境変数なしでもいいが、普通環境変数指定するよね)

```
GOOSE_DRIVER=postgres
GOOSE_DBSTRING=postgres://admin:password@localhost:5432/admin_db
GOOSE_MIGRATION_DIR=./migrations
```

最低限上の3つが必要。

`GOOSE_DRIVER`接続するデータベースに応じて。

`GOOSE_DBSTRING`データベース接続設定。<データベース種類>://<ユーザー>:<パスワード>@</url/>/<データベース>


## マイグレーション

### ファイルの書き方

`.sql`のファイルを作る。

```bash
 goose create add_some_column sql
```

で例が作られる。これを基本参考にする。

`-- +goose Up`より下が、更新する時のsqlを書く。

`-- +goose Down`が戻る時の処理を書く。何も無ければ戻るときにも何もしない。

### ファイル命名規則

`202604251200_create_auth_tables.sql`のように、タイムスタンプ形式。連番もあるが、あまり使わない。

年月日時刻_discription.sqlが基本。バージョンと中身を表すのがセット。

年月日時刻がversionになる。

### コマンド

`goose up`

マイグレーションを行う。まだマイグレーションしていないファイルが複数ある場合は、全て行う。

`goose up-to <version>`

特定のファイルまでマイグレーションする。up で全部ではなく途中までやりたい場合。

`goose up-by-one`

一つのファイルだけマイグレーションする。

`goose down`

一つだけマイグレーションを戻す。

`goose down-to <version>`

特定のファイルまでマイグレーションを巻き戻す。

`goose status`

現在のマイグレーション状況を確認する。

## 参考

1. [GitHub - pressly/goose: A database migration tool. Supports SQL migrations and Go functions. · GitHub](https://github.com/pressly/goose)
2. [Overview - pressly/goose](https://pressly.github.io/goose/)
