---
title: Ubuntu
tags:
  - 2024/06
  - Linux
created: 2024-06-15
updated: 2026-04-13
---
## 基本コマンド

### ファイル・ストレージ管理

ストレージ使用量確認  
```bash
df -h --total
```

カレントディレクトリ以下 1段階のディレクトリサイズをソートして表示

```bash
sudo du -h --max-depth=1 | sort -hr
```

 ゴミ箱の場所は基本`$HOME/.local/share/Trash/`ここになければ
 
 ```bash
 echo $XDG_DATA_HOME/Trash
 ```
 
[3]参照

ゴミ箱管理には trash が便利

```bash
sudo apt install trash-cli
```

```
trash-empty 30
```

↑で30日より古いものを削除

## 設定

### 日本語入力

fcitxでやる方法とibusでやる方法がある。どちらも利便性など大きな差はない。

mozcは日本語の入力エンジンでfcitxやibusは入力切り替えを行う。そのためfcitxだけだと日本語を入力することはできない。同様にmozcだけでは入力切替できないので日本語と半角英数を切り替えることができない。

fcitxでやる場合

```bash
sudo apt install fcitx5-mozc
```

これでfcitxとmozcが一緒にインストールされる。fcitx-入力設定 みたいなのを立ち上げると半角英数のみの入力設定になっているのでmozcを追加する。

必要な場合はfcitxの方で入力切替のキーを設定する。

もろもろの設定をした後、本体の再起動をすると入力切替が有効になる。

### フォント

標準だと日本語フォントが少ないのでとりあえず以下のものはインストールしておく。

[Takao Fonts](https://launchpad.net/takao-fonts)

```bash
sudo apt install fonts-takao
```

[IPAex フォント Ver.004.01 \| 一般社団法人 文字情報技術促進協議会](https://moji.or.jp/ipafont/ipaex00401/)

```bash
sudo apt install fonts-ipafont fonts-ipaexfont
```

フォントのインストール後はキャッシュを更新しておく。

```bash
sudo fc-cache -fv
```

### 環境変数

```sh
export PATH=$PATH:/usr/local/go/bin
```

↑こんな感じでexportコマンドで変更する。ただしこの変更はそのセッション内のみで有効である。そのため永続的に変更したい場合(大体はこれだと思うが)`.bashrc`などセッション立ち上げ時に読み込まれるファイルに書き込む。

```sh
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

さっきのを書き込もうと思うと↑の用になる。そのセッション内ですぐに反映させるために`.bashrc`を読み込む。

基本的には
1. `export`で挙動を確認、うまくいけば
2. `.bashrc`に書き込む

### ネットワーク

[ubuntu-server]({{% relref "/60_Manual_2/64_OS/ubuntu-server" %}}#network)も参照。

nmcli:NetworkManagerをいじるためのCLI。

```sh
nmcli device #ネットワークデバイスの一覧とその接続状況
nmcli connection #設定されている接続一覧とその接続状況
```

nmtui：ちょっといい感じのTUI(text user interface)でNetworkManagerをいじれる。GUIより見やすかったりするので基本これでやるのはあり。

ネットワーク設定がうまくいかず初期化したいときは、GUIで接続設定を削除するだけでなく、`/etc/netplan`の中のファイルを全削除する。GUIで消えきらないものも消せる。

`01-network-manager-all.yaml`以外のファイルを削除してネットワークマネジャーの再起動をして↓GUIやnmtuiで接続設定を加えればいい感じになる。

```sh
sudo systemctl restart NetworkManager
```

ファイル構成

`01-network-manager-all.yaml`:レンダラーをNetworkManagerに設定するファイル。基本的にファイルの中身は↓と同じ。そのため実際にはこれ以外のファイルを消せばいい。

```yaml
network:  
 version: 2  
 renderer: NetworkManager
```

`90-NM-<接続ごとの文字列>.yaml`:接続設定一つごとに一つ作られる。中を見ればなんとなくでアドレス設定とかゲートウェイ設定をどうすればいいかはわかる。GUIで適当に一つ作ってそれを編集するでも良いかも。

変更を反映させるには↓

```sh
sudo netplan apply
```

## アプリケーション管理

### 優先順位

apt で入れられるのは apt で入れておけば管理しやすいのでなるべくaptで入れる。`.deb`ファイルをダブルクリックしてアプリセンターみたいなのを起動させてインストールするとエラーが起きることが多いが `apt install`で解決することも多いので試すこと。

apt で入れられないものは公式の推奨のアプリケーションパッケージを選ぶ。

### apt

Advanced Pacage Toolでありubuntuのアプリケーション管理の基本。基本的にはこれで管理する。

`.deb`ファイルからもインストール可能。

#### 基本コマンド

更新

```bash
sudo apt update
sudo apt upgrade -y
sudo apt autoremove -y
```

インストール　`.deb`ファイルからインストールする際には./<ファイルパス>

```bash
sudo apt install <software>
```

### snap

ubuntu公式のcanonicalが作成しているサンドボックス型のアプリケーション。Ubuntu標準のアプリセンターなどからインストールすることができる。サンドボックス型であることと自動アップデートが特徴。systemdを前提として動くのでmxlinuxのようなsystemdを使っていないlinuxでは使えない。常時起動させておくようなソフト(Discordなど)だと、起動中はアップデートできない関係で通知がずっときてうるさい。バージョン管理などは向いていない。

obsidian等の日本語入力ができないソフトウェアがいくつかある。

### Appimage

サンドボックス型。`.Appimage`のファイル一つで起動させられるので一番手軽に使える。USBに入れて他のPCに入れることも可能。ただしバージョンの更新の際には再度ファイル全体のダウンロードが必要となる。とりあえず試すときなどに便利。

### Flatpak

snap同様サンドボックス型。snap よりも安定感があるような(気がする)。

インストール

```bash
sudo apt install flatpak
```

リポジトリ登録

```bash
flatpak remote-add --if-not-exists flathub https://dl.flathub.org/repo/flathub.flatpakrepo
```

リポジトリ登録後再起動。

## ドライバー関連

### GPU

ゲームしなくてもCPUの負担が減って快適になるので汎用ではなくプロプライエタリを入れるほうがいい。==GPUドライバーを変更する前にTimeshiftでバックアップをとれ。==

今使っているドライバーの確認方法。

```sh
lspci |grep -i amd
```

↑でgpuを探す。grep は nvidia か amd か radeon で大体出る。

```sh
05:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Ellesmere [Radeon RX 470/480/570/570X/580/580X/590] (rev ef)
```

それっぽいのが見つかるので↑id 指定して更に -v オプションで詳しく情報を見る。

```sh
lspci -s 05:00.0 -v  
05:00.0 VGA compatible controller: Advanced Micro Devices, Inc. [AMD/ATI] Ellesmere [Radeon RX 470/480/570/570X/580/580X/590] (rev ef) (prog-if 00 [VGA controller])  
       Subsystem: Micro-Star International Co., Ltd. [MSI] Radeon RX 570 Armor 8G OC  
       Flags: bus master, fast devsel, latency 0, IRQ 73  
       Memory at d0000000 (64-bit, prefetchable) [size=256M]  
       Memory at e0000000 (64-bit, prefetchable) [size=2M]  
       I/O ports at e000 [size=256]  
       Memory at fce00000 (32-bit, non-prefetchable) [size=256K]  
       Expansion ROM at 000c0000 [disabled] [size=128K]  
       Capabilities: <access denied>  
       Kernel driver in use: amdgpu  
       Kernel modules: amdgpu
```

使っているのがRX570でドライバーはamdgpuが使われているのがわかる。

#### NVIDIA

[NVIDIA 公式ドライバーのダウンロード \| NVIDIA](https://www.nvidia.com/ja-jp/drivers/)

↑linuxのドライバーをここから選ぶ(2025/03/18参照)。[Unix Drivers \| NVIDIA](https://www.nvidia.com/en-us/drivers/unix/)推奨されたものをここから選ぶ。`.run`ファイルがダウンロードできるので

```bash
sudo bash <file>.run
```

でインストールが始まる。対話的に進められるので適宜選ぶ。==適当にEnterを押すな==。終わったら再起動する。

これで今のところは問題なくドライバーがインストールできている。ドライバーと一緒にNVIDIA-server-settings 的なGPUのタスクマネージャーみたいなのもインストールされておりこれで使用率、温度を見ることができる。

GPUの使用率や温度を見るには↓コマンド

```bash
watch -n 0.5nvidia-smi
```

aptで勝手に入れてくれるのを祈る方法もある。

```bash
sudo ubuntu-drivers autoinstall
```

#### AMD

[AMD Radeon™ & Radeon PRO™ グラフィックス用 Linux® ドライバー](https://www.amd.com/ja/support/download/linux-drivers.html)

↑のwith ROCmにあるコマンドをポチポチする。特に選択などなく、処理が終わったら再起動するとドライバーがあたる。`./opt/rocm/bin/clinfo`で正しくドライバーが当たっていればGPUやドライバーの情報がでる。

amdgpuのドライバーはubuntu側が事前に持っているので何もしなくてもGPUを挿して起動すればドライバーがamdgpuになっていることも多いが、↑のROCmコマンドをポチポチしないと最新の正確なドライバーが全部インストールされるわけではないのでドライバーが提要されている用に見えてもやったほうがよき。

ドライバーを変更後、Wayland環境では起動できなくなった。~~またモニターのスピーカー出力にノイズ、途切れが発生するようになった。これはどうしようもないのか。~~ GPU二枚挿しをやめたら直った。変なことはやるなってことだね。

メモ：MSI RX570はコマンド適用すると映らなくなる。だめ。(2025/07/04 Ubuntu24.04)

#### ミスったら

まず水を飲む。落ち着く。とりあえずCLIを映す所から始めよう。

起動してメーカーロゴ出た後あたりでshitを押しっぱなしにするとubuntuの起動選択がでる。うまく行かなくても5回ぐらいやれば出る。あきらめるな。

CLIにはいったらドライバーをゴニョゴニョして回復させる方法もあるがさっさとTimeshitからバックアップしたほうがいい。

```sh
timeshift -h
```

↑これをすればやるべきことはほとんどわかる。

## 参考

1. [「Flatpak」でUbuntuに最新アプリをインストールする方法 \| LFI](https://linuxfan.info/flatpak-ubuntu)
2. [Flatpak—the future of application distribution](https://flatpak.org)
3. [\[Linux\] ゴミ箱に関する調査メモ Linux - Qiita](https://qiita.com/redh00k/items/1e56d8bfd9e4e011f61c)
