---
title: node_js
tags:
  - 2024/11
  - JavaScript
  - npm
created: 2024-11-02
updated: 2026-02-05
---
javascriptの実行環境。nord.jsもあるの間違いの原因すぎるだろ。

## install

[Node.js — Node.js Releases](https://nodejs.org/en/about/previous-releases)

versionについて。ubuntuみたいな定期的なアップデートとlong term support(LTS)の仕組み。バージョンは年2回更新で偶数が4月、奇数が10月。偶数のがLTSにあたり2.5年間サポートされる。最新機能とかそこまでしっかり追うんじゃなければ基本、その時の偶数の最新にしておけばいいかと。サポート切れにならないようにだけ気をつけよう。

[Node.js — Download Node.js®](https://nodejs.org/en/download/package-manager/current)
↑公式に従ってインストール。

手順としてはNode Version Manager(nvm)をインストールしてnvmによってNode.jsをインストールする。nvm?↓

[GitHub - nvm-sh/nvm: Node Version Manager - POSIX-compliant bash script to manage multiple active node.js versions](https://github.com/nvm-sh/nvm)

nvmをインストールしたら`source .bashrc`すること。もしくはターミナルの再起動。

## 参考

- [Node.jsとはなにか？なぜみんな使っているのか？ JavaScript - Qiita](https://qiita.com/non_cal/items/a8fee0b7ad96e67713eb)
- [Node.js — Run JavaScript Everywhere](https://nodejs.org/en)
- [npm installの「npm」って何? JavaScript - Qiita](https://qiita.com/nolanlover0527/items/2c61292a731af6020730)
