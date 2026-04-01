---
title: flyway
tags:
  - 2025/09
  - データベース
created: 2025-09-18
updated: 2026-03-17
draft: false
---
データベースマイグレーションツール

## インストール

[Command-line - Redgate Flyway - Product Documentation](https://documentation.red-gate.com/fd/command-line-277579359.html)

```bash
 wget -qO- https://download.red-gate.com/maven/release/com/redgate/flyway/flyway-commandline/11.13.1/**flyway-commandline-11.13.1-linux-x64.tar.gz** | tar -xvz && sudo ln -s `pwd`/flyway-11.13.1/flyway /usr/local/bin
```

↑現在のディレクトリにflywayディレクトリをダウンロードしてシンボリックリンクでパスがそこに通っているようになる。そのためflywayディレクトリを移動させるときはそのシンボリックリンクも変更するのを忘れずに。

## 作業フロー

`flyway.conf`を作業ディレクトリに作成

```flyway.conf
flyway.url=jdbc:postgresql://localhost:5432/specimen_db  
  
flyway.user=saku  
  
flyway.password=14afqrzv  
  
flyway.locations=filesystem:./migrate  
  
flyway.schemas=public
```

マイグレート用のsqlファイルを作成

`flyway info`で一応確認。修正。

`flyway migrate`でマイグレーション。

## コマンドリスト

```bash
flyway info
```

とりあえず確認。エラー出たら対処。


## 参考

1. 
