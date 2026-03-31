---
title: MXLinux
tags:
  - 2024/05
  - Linux
  - Linux/MXLinux
  - Snap
created: 2024-05-30
updated: 2025-08-31
date: 2024-05-30
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# MX Linux

MXLinuxをメインPC/ノートPCとして使っていく上でのメモ。

## 環境

### OS

バージョン確認
```bash
cat /proc/version
```

### ハードウェア

laptop
- CPU : Ryzen7 5700
- RAM : 16GB
- storage : M.2 nvme 500GB

## ディレクトリ構成

他のlinux系統とほとんど変わりなくツリー構造のディレクトリ構成をしている。

### root直下の使い分け



### user直下の使い分け

(cloud)はクラウドで他のPCと共有する。

- Desktop : とりあえずの保管場所。Downloadsよりも長期的に入れておきたいものやディレクトリごとなどで大きいものなど。
- Downloads : とりあえずファイルを入れておく場所。なるべくきれいに保つ。
- Documents(cloud) : メインのディレクトリ。hugoやobsidian、研究室関連のものなどを入れる。長期保管。[Mathematica]({{< relref "/60_Manual_2/62_Software/Mathematica" >}})など一部のソフトはデフォルトでここにファイルを保管する。
- Local_Documents : クラウド共有しないDocuments。メインPCでしか使うことのない電子書籍やTbio関連のプログラム等。
- Google(cloud) : Google drive をマウントする。
- MEGA(cloud) : MEGAで共有する用で、とりあえず入れておきたいファイルの保管場所。論文の保管場所としても使う。(zoteroでしか論文を開かない)
- Research : 研究用。論文以外。
- Templates : libreofficeのpowerpointのテンプレートを入れるくらいしか使っていない。
- program : プログラムをつくったらここに1ディレクトリ1プロジェクトで入れる。
- R, miniforge3, snap, zotero : ソフトが勝手に作る。基本触らない。

#### 隠しディレクトリ

- .ssh : sshの設定と鍵
- .config : 各種ソフトウェアの設定

## パッケージ

### MX package manager

MX公式側が用意してくれている。ほとんど中身はaptで入れるものと変わらなかったりするが細かい挙動がうまく調整されている。設定などが円滑なのでこれにあるものはこれを使う。

### snap

MXLinuxではsystemdがオプションなので基本はsnapを使えないがsystemdを起動すれば使える。なんだかんだsnapは便利なので使っている。そのうえでのいくつか注意点。
[MXLinux]({{< relref "/60_Manual_2/64_OS/MXLinux" >}}#mx-linuxでのsnapの問題)も参考に。

#### install

```
sudo apt update  
sudo apt install snapd
sudo snap install core
```

MX起動設定ツールでsnapを選択

#### 環境変数PATH

``/snap/bin``がsnapのパスなのでこれが環境変数に追加される必要がある。.bashrcの最終行に以下を追加。
```
export PATH=$PATH:/snap/bin
```
これでターミナルを再起動しても引き継がれる。

ただしこれではそのアカウントのみの環境変数しか変えれていないのでsudoでsnapが使えない問題がある。これはsudoが環境変数を引き継がないため。

sudo の設定に入る。
```
sudo su -
visudo
```
これで
```
Defaults   env_reset
Defaults   secure_path=""
```
ここをコメントアウトする。

インストール、PATHの設定が終わったら以下で確認。
```
sudo snap install hello-world  
hello-world
```

## 設定変更等
### アプリケーションダッシュボード(スタートメニュー)
表示されるアプリを管理している場所はシステム全体で利用されるものは`/usr/share/applications`、個人利用は`~/.local/share/applications`に`.desktop`ファイルで保存されている。

基本的な書式は以下の通り。
```
[Desktop Entry]
Name=Example Application
Exec=/usr/bin/example
Icon=example
Type=Application
Categories=Utility;
```
Exec に実行パスを記述。Iconに画像ファイル、Nameに表示名を設定。

#### MX Linuxでのsnapの問題
MX Linuxの場合にはsnapの`.desktop`ファイルが`/var/lib/snapd/desktop/applications`に保存されている。しかしながらこちらはアプリケーションダッシュボードに表示されないのでシンボリックリンクを作成する。

```
sudo ln -s /var/lib/snapd/desktop/applications/*.desktop /usr/share/applications/
```

`.desktop`ファイルをすべてシンボリックリンクを作成する。しかしこれだとsnap をインストールするとき毎回このコマンドを実行する必要がある。それは面倒である。ということでsnap install をしたときに毎回シンボリックリンクの作成コマンドを実行するようにしたい。けれどできなかったので結局、``/usr/share/applications/snap``のディレクトリにsnapの``.desktop``ファイルが収められることは見つけたのでそこから``/usr/share/applications/``に移動する。

そこで``snap install``にエイリアスを設定する。

```
sudo nvim ~/.bashrc
```

ただし引数をとってエイリアスを設定するのがよくわからなくて面倒になってやめた。

### GPU関連

[MX Linux(KDE)でNVIDIAドライバーをあてよう - saku Blog](https://blog.theoretical-biology.info/posts/2024/0515/)

#### AMD Radeon

[Radeon™ Software for Linux® Installation — amdgpu graphics and compute stack unknown-build documentation](https://amdgpu-install.readthedocs.io/en/latest/index.html)

「radeon ドライバー 」とかで検索するとamdの公式debファイルのダウンロードページが見つかる。ただし、そのdebファイルを何も考えずにそのままインストールするとうまく行かないことがあるので↑リンクを参考に。




### KDEconnect

```
sudo ufw allow 1714:1764/udp 
sudo ufw allow 1714:1764/tcp 
sudo ufw reload
```
これでファイアウォール設定変更したら使えるようになった。



## ハードウェアテスト

### 負荷テスト

s-tuiを使うとcpu周波数、温度を取得できる。stressでcpu使用率を100%にできるのでその時の温度が80くらいまでなら嬉しい。stressはcpu負荷をかけるソフト。ほとんどそのままs-tuiで使われてるっぽい。周波数も見れるのでサーマルスロットリングが起きてないか確認。
```
sudo apt install stress
sudo apt install s-tui
```

## 電力効率化

### Powertop

```bash
sudo apt install powertop
```

```bash
powertop
```

tabで項目切り替え。Tunablesで省電力化の各項目を設定できる。Goodは省電力設定担っている。

## 参考

- Linuxの教科書
- [MX Linux – Midweight Simple Stable Desktop OS](https://mxlinux.org)
