---
title: Debian
tags:
  - 2024/07
  - Linux
created: 2024-07-23
updated: 2025-08-17
---
## 環境構築

### ユーザー追加


```
sudo adduser <user_name>
```
パスワードを入力しそれ以外にも色々聞かれるが基本入力せずにEnterでよし。

### シェル変更

現在のシェル確認 どっちでも同じ。
```
echo $SHELL
echo $0
```

シェル変更
```
chsh -s /bin/bash
```

### プロンプトカスタマイズ

現在の設定確認。
```
echo $PS1
```
プロンプトの設定は環境変数の$PS1に入っている。これをいじることで色を変えたりする。

.bashrc, .bash_profile あたりをいじる。

```
vim ~/.bashrc
```

↓のPS1の設定はメインPCのコピー
```
PS1="\[\e]0;\u@\h: \w\a\]\[\e[1;35m\]\u\[\e[0m\]@\[\e[1;36m\]\H\[\e[0m\]:\[\e[1;32m\]\w\[\e[0m\]"
export PS1;
```

```
source ~/.bashrc
```

## パッケージ関係

### apt 

更新　基本作業前にこれを脳死でやる。
```
sudo apt update
```

バージョンアップ
```
sudo apt upgrade 
```

インストール
```
sudo apt install <package>
```

アンインストール
```
sudo apt remove <package>
```
完全アンインストール アンインストールだけでは消さない設定ファイルも消すことがある。
```
sudo apt purge <package>
```

インストール候補一覧
```
sudo apt list <package> -a
```

パッケージ情報
```
sudo apt info <package>
```

## 設定

### Wake-on-Lan

#### 受信側

```
ethtool [インターフェース名] | grep "Wake-on"
```

これでWake-on-Lanが有効かどうかがわかる。`Wake-on: d`または`Wake-on: g`が表示されれば、WOLが有効。

無効の場合、BIOS,UEFIで有効化する。

#### 送信側

```
sudo apt install wakeonlan
```

パッケージインストール。

```
wakeonlan [MACアドレス]
```

起動コマンド。MACアドレスは`ifconfig`で確認する。

```
wakeonlan 4c:cc:6a:2b:9c:3d
```

## 参考

- [bashターミナルプロンプトの表示・色の変更｜くりログ](https://lecu1012.com/bash_terminal_customize/)
