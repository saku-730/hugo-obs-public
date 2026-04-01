---
title: WINE
tags:
  - 2025/06
created: 2025-06-23
updated: 2025-08-31
---
Wine Is Not an Emulator

## Install

[Debian/Ubuntu · Wiki · wine / wine · GitLab](https://gitlab.winehq.org/wine/wine/-/wikis/Debian-Ubuntu)基本このサイト通りで。

32 bit アーキテクチャの有効化

```bash
sudo dpkg --add-architecture i386
```

リポジトリキーの登録とダウンロード

```bash
sudo mkdir -pm755 /etc/apt/keyrings
wget -O - https://dl.winehq.org/wine-builds/winehq.key | sudo gpg --dearmor -o /etc/apt/keyrings/winehq-archive.key -
```

リポジトリの登録(バージョンにより異なるので注意)

```bash
sudo wget -NP /etc/apt/sources.list.d/ https://dl.winehq.org/wine-builds/ubuntu/dists/noble/winehq-noble.sources
```

安定版のインストール。

```bash
sudo apt update
sudo apt install --install-recommends winehq-stable
```

## Winetricks

[Winetricks · Wiki · wine / wine · GitLab](https://gitlab.winehq.org/wine/wine/-/wikis/Winetricks)

WinetricksはWine実行に必要だったりするスクリプト群。

Discoverからインストール可能。とりあえず入れとけ的プログラム。

### 豆腐文字化け対処

日本語を始めとする2バイト文字はデフォルトでは豆腐文字化けしてしまうのでCJKフォントをインストールする。インストール後はWineを再起動して変更を適用する。

```bash
winetricks cjkfonts
wineserver -k && wineboot
```

## 参考

1. [WineHQ - Run Windows applications on Linux, BSD, Solaris and macOS](https://www.winehq.org)
2. [Winetricks · Wiki · wine / wine · GitLab](https://gitlab.winehq.org/wine/wine/-/wikis/Winetricks)
3. [Wineで日本語フォントが正しく表示されるようにする](https://zenn.dev/nemolize/articles/26c21148286705)
