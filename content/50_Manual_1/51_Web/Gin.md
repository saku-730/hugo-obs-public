---
title: Gin
tags:
  - 2025/07
  - Go
created: 2025-07-08
updated: 2026-01-22
---
## Install

[Quickstart \| Gin Web Framework](https://gin-gonic.com/en/docs/quickstart/)

を参考に始める。

## ミドルウェア

Ginの特徴の一つ。httpリクエストがきてハンドラーに到達する前、または色々バックエンドが処理してハンドラーが返すときのハンドラーのあとに行う処理たち。バックエンドの処理を行う前/後に毎回行うことになる。

ログ記録など毎回のように行う必要がある処理はハンドラーそれぞれに書くよりもミドルウェアとして書いたほうが色々整理されていいよねっていうのが一番の利点。

## CORS

公式のミドルウェアがあるのでそれを使う。

[GitHub - gin-contrib/cors: Official CORS gin's middleware](https://github.com/gin-contrib/cors)

## 参考

1. [Gin Web Framework \| Gin Web Framework](https://gin-gonic.com/ja/)
2. [Ginフレームワークミドルウェア詳細：ロギングからリカバリーまで \| Leapcell](https://jp.leapcell.io/blog/gin-framework-middleware-deep-dive-from-logging-to-recovery)
