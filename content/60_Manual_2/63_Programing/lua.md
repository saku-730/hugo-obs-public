---
title: lua
tags:
  - 2024/10
created: 2024-10-31
updated: 2025-08-31
---
きっかけはNeovimでした。


## インストール

必要ないことのほうが多かったり。

バージョン確認↓
```
sudo apt list lua5* -a
```
特に古すぎたりしなければ
```
sudo apt update; sudo apt install lua<version>
```

aptが古かったら公式からtarをダウンロードしてbuildする。

## 書き方 基本

### 変数

基本は=でグローバル変数が作られる。型宣言は不要
```lua
x=12
```

ローカルでの変数宣言にはlocalをつかう。
```lua
x = 12
```
ローカルでも関数から参照できるのであまり意味がない? 関数内ではlocalをつけたほうが安全である。　

データ型の種類

- nil: 値が存在しないことを表す
- boolean: trueまたはfalseの値を表す
- number: 数値を表す
- string: 文字列を表す
- function: 関数を表す
- table: テーブルを表す（配列や連想配列など、複数の値をまとめて扱うデータ構造）

### 演算子

四則演算は通常の + - * / 

### 制御構文

#### 条件分岐 if



### その他

コメント
```lua
-- 1行コメント 
--複数行コメント --
```

文字出力はprint
```lua
print("Hello world")
```

##  参考

- [The Programming Language Lua](https://www.lua.org/home.html)
- [Lua/チュートリアル - Wikibooks](https://ja.wikibooks.org/wiki/Lua/%E3%83%81%E3%83%A5%E3%83%BC%E3%83%88%E3%83%AA%E3%82%A2%E3%83%AB)
