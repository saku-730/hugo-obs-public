---
title: Rust
tags:
  - 2026/03
created: 2026-03-19
updated: 2026-03-30
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Rust

## 環境構築

インストール

```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

最新は[Rust をインストール - Rustプログラミング言語](https://rust-lang.org/ja/tools/install/)で確認

インストール種類を聞かれたら、standardにする。

```bash
source "$HOME/.cargo/env"
rustc --version  
cargo --version
```

バージョン見えればインストール成功。



## 参考

1. [Rustプログラミング言語](https://rust-lang.org/ja/)
2. [The Rust Programming Language 日本語版 - The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/title-page.html)