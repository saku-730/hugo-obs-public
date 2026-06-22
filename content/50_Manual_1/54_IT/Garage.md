---
title: Garage
tags:
  - 2026/06
  - AWS
  - S3
  - Storage
created: 2026-06-22
updated: 2026-06-22
draft: false
---
S3互換ストレージサーバー

## インストール

[Downloads \| Garage HQ](https://garagehq.deuxfleurs.fr/download/)

ここで適切なバージョンのバイナリをダウンロード。

拡張子を消して、保存。保存場所は色々あるがおすすめは、`/opt`以下に実態ファイルはおいておいて、シンボリックリンクで`/usr/bin`以下に作る方法。

Garage binary は `/opt/garage/versions/{version}/garage` にバージョンごとに配置する
実行パスは `/usr/local/bin/garage` から対象バージョンの binary へ symlink する

 例: 
```
/opt/garage/versions/v2.3.0/garage
/usr/local/bin/garage -> /opt/garage/versions/v2.3.0/garage
```

```bash
garage --version
```

## 設定

開発時はリポジトリ直下で次のコマンドを実行して Garage server を起動する。

```bash
GARAGE_CONFIG_FILE=./garage/garage.toml garage server
```

```bash
GARAGE_CONFIG_FILE=./garage/garage.toml garage layout assign -z home -c 10G 165e
```

とりあえず10Gストレージを割り当てる。

```bash
GARAGE_CONFIG_FILE=./garage/garage.toml garage layout apply --version 1
```

設定反映

```bash
GARAGE_CONFIG_FILE=./garage/garage.toml garage bucket create occurrence-media
GARAGE_CONFIG_FILE=./garage/garage.toml garage key create occurrence-web
```

バケットとアクセスキーの作成

## 参考

1. 
