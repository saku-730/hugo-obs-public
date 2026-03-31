---
title: zola
tags:
  - 2025/07
  - SSG
created: 2025-07-02
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# zola

## Install

[Installation \| Zola](https://www.getzola.org/documentation/getting-started/installation/)

Ubuntu推奨は特になかったのでsnapで。

```sh
sudo snap install --edge zola
```

## ファイル構造

```
├── config.toml ## zolaの設定ファイル
├── public ## ビルドされたファイル
├── content ## htmlと紐づくMarkdownファイルなど
├── sass ## scssファイル
├── static ## ファビコンなどの静的なコンテンツの置き場
├── templates ## ページを構成するhtml置き場
└── themes ## 提供されているサイトのテーマなどを格納する場所
```
参考[2]より

### トップページ

## テーマ

[HUGOBlog]({{< relref "50_Manual_1/51_Web/HUGOBlog.md" >}})と同じような感じ。

導入方法は
1. `themes`ディレクトリに移動して`git clone `でテーマのリポジトリをダウンロード
2. `config.toml`の`theme = `を書き換え。このときの値はテーマのディレクトリ名。

基本はこれだけだが==`templates`ディレクトリがあるとそれを優先してしまってテーマが適用されない。==
そのため`templates`ディレクトリを削除するか、書くテンプレートファイルの先頭に`{% extends "テーマ名/templates/元のファイル名" %}`を書いてテーマを継承しながら自分の作ったテンプレートも適合させる。

テーマそのままでいいなら`templates`ディレクトリを削除するのが一番楽。そのとき、すでに作成済みの`md`ファイルがもとのテンプレートを読み込む設定をしているならそれも消す。

## 参考

1. [Zola](https://www.getzola.org)
2. [Rust製SSGのZolaでブログを構築する](https://zenn.dev/ryokatsu/articles/3186fc7166b087)