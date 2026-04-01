---
title: Next-js
tags:
  - 2025/02
  - JavaScript
created: 2025-02-18
updated: 2026-01-22
---
## インストール

[node_js]({{% relref "/50_Manual_1/51_Web/node_js" %}})のインストールが必要。

## ディレクトリ構造

app router と pages router の２つの仕組みがある。バージョン13くらいからapp routerが導入された。この２つのディレクトリ構造の違いによって大きく設定が異なる場合もあるのでwebでの情報などはどちらを使っているのか注意すること。なおこの記事ではapp routerを基本とする。

## 基本コマンド

サーバー立ち上げ
```
npm run dev
```
```
http://localhost:3000
```
にサイトが立ち上がる

依存パッケージインストール

```bash
npm install
```

git pullした後などはパッケージを↑で入れる。

## サイト構築

↓でサイトの最初の一歩がはじまる。カレントディレクトリの下にプロジェクトディレクトリを作る。
```bash
npx create-next-app@latest  
Need to install the following packages:  
create-next-app@15.0.2  
Ok to proceed? (y) y  
  
✔ What is your project named? … glossary  
✔ Would you like to use TypeScript? …  Yes  
✔ Would you like to use ESLint? … Yes  
✔ Would you like to use Tailwind CSS? …  Yes  
✔ Would you like your code inside a `src/` directory? …  Yes  
✔ Would you like to use App Router? (recommended) …  Yes  
✔ Would you like to use Turbopack for next dev? …  Yes  
✔ Would you like to customize the import alias (@/* by default)? …  Yes  
✔ What import alias would you like configured? … @/*
```

↓でサイトをlocalhost:3000で建てる。ブラウザで開けたらちゃんとできてる。
```bash
npm run dev
```

### Routing

terminology-component-tree.avif
[Building Your Application: Routing | Next.js](https://nextjs.org/docs/app/building-your-application/routing)より(2024/11/3)

terminology-url-anatomy.avif
[Building Your Application: Routing | Next.js](https://nextjs.org/docs/app/building-your-application/routing)より(2024/11/3)

基本はツリー構造。URLはツリーの構造に即したもの。hugoとかと同じでわかりやすいよねっていう感じ。`dashboard/settings/profile/page.js`のURLは`dashboard/settings/profile`になる。`page.js`か`route.js`のみ表示される。ここもhugoでのリーフ構造にちかい。そのためサイト表示につかうならリーフディレクトリには`page.js`を含む必要がある。


app Router は version13 から導入された pages よりも優先される仕組み。いまはこれが推奨。`app`ディレクトリをルートにする。

## Markdown 

Next.jsではもちろんmarkdown→htmlにも対応している。

### react-markdown

一番始めに候補に上がるプログラム。

#### tailwindcss-typography

[GitHub - tailwindlabs/tailwindcss-typography: Beautiful typographic defaults for HTML you don't control.](https://github.com/tailwindlabs/tailwindcss-typography)

## デザイン

## 個別ページ

### エラーページ

デフォルトでnext.jsが準備してくれているものもあるがトップページに戻るリンクがなかったりサイトデザインが大きく違ったりするので基本的には簡単なものでいいので新たに作ること。

404 notfound

`app/not-found.tsx`を作成する。位置に注意

## 参考

1. [Next.js 日本語ドキュメント](https://nextjsjp.org)
2. [Next.jsでオリジナルエラーページを作ってみよう](https://zenn.dev/megane_s/articles/8ecc608f9544d4)
3. 
