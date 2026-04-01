---
title: PROXMOX
tags:
  - 2025/06
created: 2025-06-15
updated: 2026-03-17
---
仮想化環境つくりたり

## 設定

### 初期設定

サブスクリプションポップアップの消去

```bash
sed -i.bak "s/data.status !== 'Active'/false/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js
```

参照するリポジトリの変更

エンタープライズリポジトリをデフォルトでは参照しているのでサブスクリプションなしのリポジトリに変更。

`etc/apt/sources.list.d/pve-enterprise.list`を変更。コメントアウトする。

```
# deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

`etc/apt/sources.list`を変更。リポジトリを追加。

```
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
```

更新(そこそこ時間かかる)

```bash
apt update
apt dist-upgrade -y
```

### ファイアウォール

インターネット接続を制御する際に設定する。ただし例外設定ルールを作ってから実行しないとWebUIも繋がらなくなるので注意。

1. データセンター＞ファイアウォール からルールを以下の内容で追加する。

送信方向:in, 動作:ACCEPT, 有効:ON, プロトコル:TCP, ソース:接続元PCのIP, Dest.port: 8006(webUIのポート)

それ以外は空欄でOK

2. データセンター>ファイアウォール>オプション からファイアウォールを有効にする。

## 参考

1. [Proxmox VE Documentation Index](https://pve.proxmox.com/pve-docs/)
