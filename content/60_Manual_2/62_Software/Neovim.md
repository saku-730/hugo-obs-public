---
title: Neovim
tags:
  - 2024/06
  - Text_editor
  - VSCode
  - Neovim
  - Vim
created: 2024-06-06
updated: 2026-03-30
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Neovim

emacs対vim戦争の勝者?

Vim解説含む

[GitHub - neovim/neovim: Vim-fork focused on extensibility and usability](https://github.com/neovim/neovim/tree/master)

[設定リポジトリ](https://github.com/saku-730/my-nvim/tree/main)

## install

Linuxの場合、選択肢で悩むが今の所snapでいく。aptで入れられるものはバージョンが古い。snapでだめならtarballから。

デフォルトで最低限のセットアップ済みの[kickstart-modular.nvim](https://github.com/dam9000/kickstart-modular.nvim)が使いやすいのでこれを使う。neovimディストリビューションではなくあくまで最低限の設定とプラグインが入っているもので作成者の意図としてもこれを元に各自設定を詰めていってほしいというもの。modularじゃない普通のkickstartはプラグインの設定変更がだるい。

### snap
バージョンを確認↓
[Releases · neovim/neovim](https://github.com/neovim/neovim/releases)
```
snap info nvim
```
バージョンがよければこれでいく。だめなら次のTarball

snapからインストール、バージョン確認
```
sudo snap install nvim --classic
neovim --version
```

パスの確認
```
which nvim
```
今回は``/snap/bin/nvim ``

### Tarball

ファイルダウンロード　バージョンによってリンクを変えること
```
wget https://github.com/neovim/neovim/releases/download/v0.10.0/nvim-linux64.tar.gz
```

ファイル解凍
```
tar xzvf nvim-linux64.tar.gz
```

ファイル移動、実行ファイル(バイナリ)をシンボリックリンクとして配置
```
sudo mv nvim-linux64 /usr/local/nvim
sudo ln -s /usr/local/nvim/bin/nvim /usr/bin/nvim
```

以下、バージョン確認等はsnap同じ。

## コマンド

### 編集

置換
```
:%s/置換前/置換後/g
```

検索
```
/検索文字列  
?検索文字列
```


## ファイル構造

設定ファイルは`~/.config/nvim`にすべて含む。

/nvim
├── init.lua
└── lua
    ├── keymaps.lua
    ├── kickstart
    │   ├── health.lua
    │   └── plugins
    ├── lazy-bootstrap.lua
    ├── lazy-plugins.lua
    ├── options.lua
    └── plugins

- init.lua : 基本の設定ファイル。ただし設定が増えると一つのファイルで長すぎてしまうので以下のlazy-bootstrap.lua, lazy-plugins.lua, options.lua, keymaps.lua の4つのファイルに分ける。これらの読み込みを行っている。
- keymaps.lua : キーマップの設定ファイル
- lazy-bootstrap.lua : プラグイン管理のlazyを読み込む。
- lazy-plugins.lua : プラグインを読み込む。
- options.lua : 設定を書き込む。leader key や行番号の表示など。

## キーマップ

`keymaps.lua`に書く。

leaderキーとしてスペースを設定

```lua
vim.g.mapleader = ' '
```

```lua
vim.keymap.set(mode, lhs, rhs, opts)
```

optsに`(desc="explanation")`としておくと後々見返したときにわかりやすい。

## オプション設定

options.luaにプラグインやキーマップ以外の設定を書く。

### クリップボード連携

nvimのヤンク/ペーストとクリップボードを連携させる。

ターミナルとクリップボードの連携をできるようにするソフトのインストール↓

```bash
sudo apt update
sudo apt install xclip
```

`options.lua`に↓を追記

```lua
vim.opt.clipboard:append({"unnamedplus"})
```

## プラグイン

### プラグイン管理

参考[4]

[Getting Started | LazyVim](https://www.lazyvim.org)を使う。`initi.lua`にlazyが入っているか確認して入っていなければインストールするスクリプトを書く。

```lua
local lazypath = vim.fn.stdpath("data") .. "/lazy/lazy.nvim"
if not (vim.uv or vim.loop).fs_stat(lazypath) then
  vim.fn.system({
    "git",
    "clone",
    "--filter=blob:none",
    "https://github.com/folke/lazy.nvim.git",
    "--branch=stable", -- latest stable release
    lazypath,
  })
end
vim.opt.rtp:prepend(lazypath)
```

pluginsディレクトリにプラグイン一つに対して一つの.luaファイルを作成しそれをlazy-plugins.luaで読み込んでいる。

プラグインのインストールの際にはpluginsディレクトリに.luaファイルの作成する。この.luaファイルにプラグインの設定なども書く。その読み取りをlazy-plugins.luaに追記する。:Lazyを起動してインストールやアップデートを行う。

各プラグインファイルの書き方↓

```lua
return{
  "shellRaining/hlchunk.nvim", -- プラグイン名
  event = { "BufReadPre", "BufNewFile" }, -- プラグインのインストール時点での設定を書く
  config = function() --定形 これで設定を書けるようになる
	require("hlchunk").setup({ -- 以下設定を書く
		chunk = {
		    enable = true,
		    chars = {
			 horizontal_line = "─",
			 vertical_line = "│",
			 left_top = "╭",
			 left_bottom = "╰",
			 right_arrow = ">",
		    },
		    style = "#806d9c",
		},
	})
  end, --configの終わりを忘れずに書く
}
```


### プラグイン一覧

#### [nvim-neo-tree.](https://github.com/nvim-neo-tree/neo-tree.nvim)

ファイラー。`Neotree`で左側にサイドバーを展開する。さすがにだるいのでキーマップで`space + e`に設定中。

ショートカット
- `Shift + h`:隠れファイル・ディレクトリの表示/非表示を切り替え。
- a:ファイル/ディレクトリ作成
- r:ファイル名変更
- d:ファイル/ディレクトリ削除
- i:情報表示

依存プラグイン

- nui.nvim:UIコンポーネント
- plenary.nvim:バックエンド
- nvim-web-devicons:ファイルアイコン
- nvim-lsp-file-operations:LSP関係
- nvim-window-picker:

#### [hlchunk.nvim](https://github.com/shellRaining/hlchunk.nvim)

インデントとかを見やすくする系。

#### [lualine](https://github.com/nvim-lualine/lualine.nvim)

ステータスラインを見やすくする系

依存プラグイン

- nvim-web-devicons:ファイルアイコン

#### [catppuccin](https://github.com/catppuccin/nvim)

色をいい感じにする。

## LSP

`lsp.lua`に基本的には設定を追加していく。
言語ごとの個別設定は`lsp/rust.lua`などのように言語別にファイル作成。

### [nvim-lspconfig](https://github.com/neovim/nvim-lspconfig)

nvim用のlsp設定のテンプレ集のようなプラグイン。とりあえずこれを入れておく。

### LUA

[Lua Language Server \| Home](https://luals.github.io/#neovim-install)

install ↓

```bash
mise use aqua:LuaLS/lua-language-server
lua-language-server --version
```

### Rust

[GitHub - rust-lang/rust-analyzer: A Rust compiler front-end for IDEs · GitHub](https://github.com/rust-lang/rust-analyzer)



## VSCode_Neovim

[VSCode]({{% relref "/60_Manual_2/62_Software/VSCode" %}})でNeovimを使えるようにする拡張機能。vimのキーバインドにするのではなく裏側でNeovim自体を起動して使う。

設定の↓をインストール後確認したパスに編集する。同期しないようにしておく。VSCodeを使うのが基本的にLinuxでNeovimのバスが一致するなら同期しても問題ないか。

Vscode-neovim › Neovim Executable Paths: Linux

## 参考

1. [GitHub - dam9000/kickstart-modular.nvim: A launch point for your personal nvim configuration](https://github.com/dam9000/kickstart-modular.nvim)
2. [🚀 Getting Started | LazyVim](https://www.lazyvim.org)
3. [来年もneovimを使い続けるためのおすすめ設定](https://zenn.dev/hidehic0/articles/6bde5d5398384a#ui%E3%81%AE%E8%A8%AD%E5%AE%9A)
4. [lazy.nvimのインストール方法と使い方](https://zenn.dev/siteyo/articles/980b6205e93914)
5. [今からNeovimを始める人のLSP最短設定 (0.11, 2025-10-04現在)](https://zenn.dev/ras96/articles/4d9d9493d29c06)