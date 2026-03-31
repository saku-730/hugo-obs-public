---
title: VSCode
tags:
  - 2024/06
  - Text_editor
created: 2024-06-06
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# VSCode

テキストエディタのデファクトスタンダードなのか?

## Neovim

[GitHub - vscode-neovim/vscode-neovim: Vim mode for VSCode, powered by Neovim](https://github.com/vscode-neovim/vscode-neovim)
VSCode NeovimでNeovimをVSCodeで使える。[Neovim]({{< relref "60_Manual_2/62_Software/Neovim.md" >}}#vscode-neovim)も参照

neovimをvscodeから起動するものになっていてneovimの設定やプラグインもある程度は参照される。

設定からneovimの実行ファイルと設定ファイルのパスを設定する必要がある。場合によっては再起動が必要。

neovimの設定ファイルに関してはvscodeの設定画面から一つだけ設定するようになっており例えば`init.lua`を設定する。

## ショートカット・操作周り



## 拡張機能

### VSCode_Neovim

[VSCode]({{< relref "60_Manual_2/62_Software/VSCode.md" >}})でNeovimを使えるようにする拡張機能。vimのキーバインドにするのではなく裏側でNeovim自体を起動して使う。

設定の↓をインストール後確認したパスに編集する。同期しないようにしておく。

Vscode-neovim › Neovim Executable Paths: Linux

