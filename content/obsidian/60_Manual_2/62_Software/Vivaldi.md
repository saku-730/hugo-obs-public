---
title: Vivaldi
tags:
  - 2024/06
  - Browser
created: 2024-06-06
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Vivaldi

個人的ベストブラウザソフト。

## 同期

アカウントを設定することで別の端末でも設定等を同期できる。メモやブックマークもできるのでするべし。ただしマウスジェスチャーは同期されない。

ラボのネットワークだとクラウド判定で同期が弾かれてうまくいかないためvpnを使うとうまくいく。

## エラーメモ

### xdg-open

[KDE Plasma - KIO Client Error \| Vivaldi Forum](https://forum.vivaldi.net/topic/100113/kde-plasma-kio-client-error)
KDI環境でKIO Client Errorによってxdg-openが正常に機能しない。これによってvscodeの同期が正常に機能しなかったりする。
ソフトウェアがログインや同期のときにブラウザを利用する場合にxdg-openを使うことがあるのでこのとき問題になる。

他のブラウザでは起きていないエラーなのでそのときだけfirefox使ったりして一応対処。