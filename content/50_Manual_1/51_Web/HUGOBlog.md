---
title: HUGOBlog
tags:
  - 2024/05
  - HUGO
  - Blog
created: 2024-05-31
updated: 2026-03-31
---
作成日時: 2024-05-31 01:38 
最終更新日時:2024-05-31 01:38
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# HUGOBlog

[HUGO](https://gohugo.io)によるブログ作成におけるメモ。
集約、整理して同人誌にしたい。

## 作業フロー

1. `content`ディレクトリにマークダウンファイルを作成する。
```
hugo new content/posts/2025/0227/index.md
```
2. デプロイすることで自動でhtml化される。

## インストール

[Linux | Hugo](https://gohugo.io/installation/linux/)

```
sudo snap install hugo
```

```
sudo apt install hugo
```

aptまたはsnapで入れる。MXlinuxであれば基本的にsnapを避けたいのでapt。

aptが昔のバージョン0.123でとどまっているのでsnap推奨。

## サイト作成

```
hugo new site <site name>
```

site nameのディレクトリがつくられる。ディレクトリ作成後、gitなどの設定をしよう。

## 基本コマンド

```
hugo server
```
hugoサーバーを立ち上げる
```
http://localhost:1313
```
↑にアクセスするとサイトを見れる。マークダウンの編集はリアルタイムで反映される。1313を起動した状態でもう一度起動するなどした場合には適当なポートで立ち上がる。hugo のディレクトリで実行すること。

### テーマ

[Complete List \| Hugo Themes](https://themes.gohugo.io)

テーマを後から変えようと思うとサイトレイアウトや設定を考え直したりと面倒なので最初にテーマを決める。

あくまでオプションなのでテーマは使用せず、自分で作っていくでもいいが相当なこだわりがない限りは使わせてもらったほうが早くて楽。無料だし。

テーマの導入は各テーマのドキュメントを読むこと。

~~基本は`theme`ディレクトリにテーマのディレクトリを丸々入れる。ディレクトリ名とテーマ名を一致させて`hugo.toml`に`theme=them-name`を記入。~~

git のサブモジュールとして導入する。

```bash
git submodule add <テーマのgithubのhttp> theme/テーマ名
```


### ディレクトリ構成


## Githubで自動デプロイ

### 概要

ローカルリポジトリ上にhugoリポジトリをつくり、Github等のリモートリポジトリに更新分をpushする。Github Actionでデプロイ用のActionを作成し、push時にそのActionを動作させるようにする。

### Action


### コミットメッセージ

基本的には記事の更新日(例20240601)。ただし.yamlの編集やメニューの編集等サイト構造の編集は[Git]({{% relref "/60_Manual_2/63_Programing/Git" %}}#コミットメッセージ)を参照。

## 記事作成

### コマンド

``hugo new ファイルパス`` で新しい記事を作成。ファイルパスが長くて面倒なのでシェルスクリプトを作った。

/usr/local/bin/blog
```
#!/bin/bash  
  
cd /home/saku/Documents/blog  
  
year=$1  
today=$2  
  
if [ -z "$1" ]; then  
       year=$(date '+%Y')  
fi  
  
if [ -z "$2" ]; then  
       today=$(date '+%m%d')  
fi  
  
hugo new /home/saku/Documents/blog/content/posts/$year/$today/index.md
```

日付と年数を入れなくても今日のものを自動で入れる。変数として指定すればそれで作る。

``blog 2024 0601``のように第一変数は年、第二変数は日付

## 多言語対応

