---
title: Mathematica
tags:
  - 2024/06
created: 2024-06-06
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Mathematica

天才が作った技術計算システム。

## 資料

公式資料が豊富でこれだけでいいと思える。その代わりに公式以外の本、サイトが少ない。
[Wolfram Mathematica：最新の技術計算](https://www.wolfram.com/mathematica/)

[Wolfram Cloud](https://lab.wolframcloud.com)

## 基本文法

### 関数

関数[引数1,引数2,引数3]が基本の書き方。

### 変数

組み込みオブジェクトがAaaaみたいに大文字スタートなので==スネークケース==(参考 [Code_writing]({{< relref "/obsidian/60_Manual_2/63_Programing/Code_writing" >}}#変数名))で作成する。数字を含むことはできるが頭文字は必ずアルファベットにする。数式でみにくくなるので基本的には変数に数字を含めない。

ギリシャ文字の入力は↓
[Title Unavailable \| Site Unreachable](https://reference.wolfram.com/language/tutorial/MathematicalAndOtherNotation.html.ja)

### カッコ

- ()丸カッコ：式をまとめる
- []角カッコ：関数の引数
- {}中カッコ：リストの作成

### リスト

Mathematicaのリストの作成は{}で囲むだけ。

リストは数字、文字列、グラフ、リストなんでも含められる。リスト内で共通する必要もない。めちゃくちゃゆるい。

Range[], Reverse[], Join[], 等はそれ自体がすでにリストなので{Range[]}とするとリストのリストになってしまう。


### コメントアウト

(*コメントアウト*) で囲むことでコメントになる。キーボード・ショートカットでalt + / でもできる。復数行も同じ方法で可能。

### 行列

{}を使ってリスト(行)のリストとして作る。

```mathematica
mat = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}}
mat // MatrixForm
```

## 作業フロー

方眼レポート用紙にシャーペンで書いた数理モデルをもとにMathematicaで作ることが多いかと思う。とりあえず一つの数理モデルに関して２つのノートを作る。

１つ目はラフスケッチ的な扱いで色々入力して実際に数理モデルを精錬させていくためにつかう。ファイル名は<数理モデル名>_draft.nb とする。

2つ目は1つ目をあとから見返したときにわかるようなまとめノート。1つ目をつくりながら進めていくと序盤になにがあったのかわからなくなるといったことが避けられると思う。ファイル名は<数理モデル名>_sumary.nb とする。

数式の上のセルには、何についての数式なのかテキストセルを使って説明しておくこと。

## メモ

- Range[]は0含まず

## 参考

1. [Wolfram言語 & システム ドキュメントセンター](https://reference.wolfram.com/language/)
2. [数学表記と他の表記法—Wolfram言語ドキュメント](https://reference.wolfram.com/language/tutorial/MathematicalAndOtherNotation.html.ja)
3. 