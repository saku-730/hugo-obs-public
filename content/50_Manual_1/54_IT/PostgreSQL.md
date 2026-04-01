---
title: PostgreSQL
tags:
  - 2025/08
  - データベース
created: 2025-08-31
updated: 2026-01-22
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# PostgreSQL

## Install

```bash
sudo apt install postgresql
```

[flyway]({{% relref "/60_Manual_2/62_Software/flyway" %}})を使うためにJDBCドライバーのダウンロード

[Download \| pgJDBC](https://jdbc.postgresql.org/download/)



## 初期設定

aptでのインストールであればデータベースクラスタの作成は自動で行われている。

```bash
pg_lsclusters
```
これでデータベースクラスターの情報が出る。.fonc

データベースにログイン

```bash
sudo -u postgres psql
```

このように基本的には`psql`を使うときはユーザー指定が必要でしてしなければ現在のユーザー名で探す。そのためpcのユーザー名がposgreに存在しなければエラーになる。

ユーザー作成

```
CREATE ROLE saku WITH LOGIN PASSWORD '14afqrzv';
```

データベース作成

```
CREATE DATABASE specimen_db OWNER saku;
```

作ったデータベースに入れるか確認。

```bash
psql -h localhost -U saku -d specimen_db
```

dockerで建てているなら

```bash
docker compose exec postgres psql -U  -d
```

## コマンドリスト

データベース一覧

```
\l
```

ユーザー一覧

```
\du
```

データベースの所有者変更

```
ALTER DATABASE データベース名 OWNER TO 新しいオーナー名;
```

## 命名規則

列名、テーブル名の基本はスネークケース参照→[Code_writing]({{% relref "/60_Manual_2/63_Programing/Code_writing" %}}#変数名)

テーブル名は複数形にする。エンティティは複数形か集合名詞で表せる。

## pgAdmin

postgresqlの管理GUIソフトみたいなやつ。

### 接続

左メニューServersを右クリックで`Register > Server...` から作ったデータベースの情報を入力して接続開始。

### メモ

- ER図を作ってくれて外部キー制約やテーブルのカラム情報などわかりやすくていい

## 参考

1. [初心者・学習用にも！PostgreSQL入門（2023年版） \| PostgresWeb - ポスグレウェブ](https://postgresweb.com/introduction-to-postgresql)
2. [PostgreSQL Tutorial](https://neon.com/postgresql/tutorial)
3. [PostgreSQL: The world's most advanced open source database](https://www.postgresql.org)