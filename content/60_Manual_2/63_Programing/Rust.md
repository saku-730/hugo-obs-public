---
title: Rust
tags:
  - 2026/03
created: 2026-03-19
updated: 2026-04-25
draft: false
---
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

## 命名規則

スネークケースかアッパーキャメル

[rfcs/text/0430-finalizing-naming-conventions.md at master · rust-lang/rfcs · GitHub](https://github.com/rust-lang/rfcs/blob/master/text/0430-finalizing-naming-conventions.md)より

|Item|Convention|
|---|---|
|Crates|`snake_case` (but prefer single word)|
|Modules|`snake_case`|
|Types|`UpperCamelCase`|
|Traits|`UpperCamelCase`|
|Enum variants|`UpperCamelCase`|
|Functions|`snake_case`|
|Methods|`snake_case`|
|General constructors|`new` or `with_more_details`|
|Conversion constructors|`from_some_other_type`|
|Local variables|`snake_case`|
|Static variables|`SCREAMING_SNAKE_CASE`|
|Constant variables|`SCREAMING_SNAKE_CASE`|
|Type parameters|concise `UpperCamelCase`, usually single uppercase letter: `T`|
|Lifetimes|short, lowercase: `'a`|

## Tips

github とか。`/target`にコンパイル済ファイルが入るので、`.gitignore`でこれは外しておこう。転送ファイルが大幅に増えてしまう。

## 参考

1. [Rustプログラミング言語](https://rust-lang.org/ja/)
2. [The Rust Programming Language 日本語版 - The Rust Programming Language 日本語版](https://doc.rust-jp.rs/book-ja/title-page.html)
3. [Rust の命名規則 #Rust - Qiita](https://qiita.com/shikuno_dev/items/fc2bcdffdc4d3c3bd16b)
