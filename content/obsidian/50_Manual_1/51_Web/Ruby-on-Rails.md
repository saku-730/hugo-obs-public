---
title: Ruby-on-Rails
tags:
  - 2025/06
  - Ruby-on-Rails
created: 2025-06-30
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Ruby-on-Rails

開発者の幸福はRailsの基本的な哲学

## Install

```bash
sudo apt update
sudo apt install build-essential rustc libssl-dev libyaml-dev zlib1g-dev libgmp-dev
curl https://mise.run | sh
echo 'eval "$(~/.local/bin/mise activate)"' >> ~/.bashrc
source ~/.bashrc
mise use -g ruby@3
gem install rails
```

## 基本コマンド

サーバー起動。サーバーのディレクトリに入って↓
```bash
bin/rails server
```

```bash
bin/rails s -b 0.0.0.0
```

下のであればローカルネット内の他のpcからもアクセス可能。

http://localhost:3000 でデフォルトのRailsページが見れたら成功。

## データベース

テーブル名は単数形、それをもとに複数形の項目名をRailsが勝手につくる。

## メモ

- 

## 参考

1. [Ruby on Rails ガイド：体系的に Rails を学ぼう](https://railsguides.jp)
2. [Ruby on Rails: Compress the complexity of modern web apps](https://rubyonrails.org)