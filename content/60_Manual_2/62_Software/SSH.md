---
title: SSH
tags:
  - 2024/11
created: 2024-11-01
updated: 2026-03-17
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# SSH

Secure Shell

とりあえずサーバーをいじるときに。特に断りがなければopensshでやる。

基本の基本
```
ssh <ユーザー名>@<ipアドレス>
```

## install

多くの場合すでにインストールされているので必要ないが一応。
```
sudo apt install opnessh-client
sudo apt install opnessh-server
```

## ssh key

鍵の作り方。↓で公開鍵と秘密鍵がどちらも作られる。
```
ssh-keygen -t ed25519　-f <ファイル名>
```
-t で鍵の種類を選べる。オプション指定しないとrsaになる。ed25519が少なくとも2024/11/1現在の推奨らしい。
保存先はデフォルトだと~/.sshになる。基本はこのままでいいのでEnter。passphraseはなくてもいい。あったほうがいい。ファイル名が重なると上書きになるので注意。

.pubが公開鍵

公開鍵をサーバーに送る。
```
ssh-copy-id -i ~/.ssh/<ファイル名>.pub <ユーザー名>@<アドレス>
```
これでサーバー側の~/.ssh に公開鍵を送る。authorized_keys というファイルがなければ自動で作られそこに記録される。複数鍵を登録した場合もここに書き足されていく。

公開鍵のファイルを送るとか、コピペするといった方法もあるがssh-copy-id が一番、ミスが起こりにくく早い。

鍵の権限を変更しておく。(サーバー側)
```
chmod 600 ~/.ssh/authorized_keys
```

## ポートフォワード

```bash
ssh -L 8080:127.0.0.1:3000 ユーザー名@SSH先
```

↑ローカルの8080ポートをssh先の3000ポートに転送

シェルに入らず後ろでやるには`-N`でやる

```bash
ssh -N -L 8080:127.0.0.1:3000 ユーザー名@SSH先
```

## ssh config

ssh の設定をconfigに書くことで毎回ipアドレスを入力したりせずにホスト名だけでつなげることができるようになる。Obsidian,VSCode等のプラグインでGitを使いたいならほとんど必須である。

~/.ssh/config

```
#-----------------
Host 192.168.2.100
 HostName 192.168.2.100
 User saku

Host guppy 
 HostName 192.168.1.1
 User saku
 IdentityFile ~/.ssh/id_guppy_ed25519
 port 1111
  
Host kajiki
 HostName 192.168.1.2
 User sakuma
 IdentityFile ~/.ssh/id_ed25519

Host github.com
 HostName github.com
 IdentityFile ~/.ssh/id_rsa
 User saku
#-----------------
```

このようにしておくと例えば```ssh kajiki```だけでつながるようになる。portはデフォルトの22であれば特に書く必要がないが変更している場合には記述する。

## scp 

Secure Copy

ファイル送信 自分のpcからサーバーへ送る。
```
scp  -P (オプション:ポート番号) <送りたいファイルのパス> <ユーザー名>@<アドレス>:送りたいパス
```

ファイル受信 サーバーから自分のpcへ送る。
```
scp <ユーザー名>@<アドレス>:<送りたいファイルのパス> 送りたいパス
```

ディレクトリの場合には -r をつける。

## auto ssh

常時SSH接続しておきたい場合に使う。

```bash
sudo apt update
sudo apt install -y autossh
```

## 参考

- [SSH公開鍵認証で接続するまで ssh公開鍵認証 - Qiita](https://qiita.com/kazokmr/items/754169cfa996b24fcbf5)
- [OpenSSH Server | Ubuntu](https://ubuntu.com/server/docs/openssh-server)