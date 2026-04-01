---
title: ubuntu-server
tags:
  - 2025/07
  - Wake-On-LAN
created: 2025-07-02
updated: 2025-08-17
---
## 設定

### Wake On LAN

#### 受信側 起動側

必要ソフトのインストール

```bash
sudo apt install ethtool
```

起動する側が有効になっているかどうかを確認する。

```bash
ip add show
```
↑ これでデバイス名確認
```sh
sudo ethtool <device> |grep -i wake
```

Wake-on:d であれば無効、g であれば有効。

有効化

```
sudo ethtool -s <device> wol g
```

エラーなどで有効化できない場合はBIOS設定で有効になっていない、またはネットワークカードが対応していない。最近の有線ネットワークカードが対応していないことはほとんどないので基本的にはBIOSをいじればうまくいく。

この設定は一時的なものなので永続化させる。

`/etc/netpaln`にある`.yaml`ファイルを編集する。`50-cloud-init.yaml`など。

`wakeonlan: true`を対象のネットワークカードのところに追加。インデントに注意。

設定の変更を反映する。これでエラーがでなければ基本大丈夫。

```bash
sudo netplan apply
```

#### 送信側

ツールインストール

```sh
sudo apt install wakeonlan
```

```sh
wakeonlan <MACアドレス>
```

## Network

ネットワーク設定はUbuntu(GUI付き)でつかっている、NetworkManagerは初期状態ではインストールされていない。

一応関係性としては↓みたいな。

| | Ubuntu Desktop | Ubuntu Server |
| :--- | :--- | :--- |
| **設定ファイル** | `netplan` | `netplan` |
| **レンダラー** | `NetworkManager` | `systemd-networkd` |
| **CLI**| `nmcli(nmtui)` | `networkctl` |

ネットワーク設定は普段使っているnmcliとかnetworkmanagerを使えずやりにくいのでなるべくインストール時に設定してしまおう。まあ、netplanが書ければ同じように設定できる。`.yaml`の書式だけ気をつけよう。

## メモ

### ノートパソコンの蓋の動作

ubuntu server 用にノートパソコンを使った場合など、蓋の開閉にアクションをもたせたくない場合の設定方法。

`/etc/systemd/logind.conf`を編集する。

↓の用にコメントアウトされている。コメントアウトの内容がデフォルト内容なのでこの場合、蓋が閉じるとサスペンドする。

```
#HandleLidSwitch=suspend
```

変更するためにコメントアウトを解除して内容を ignorre に変更する。

```
HandleLidSwitch=ignore
```

設定の反映

```bash
sudo systemctl restart systemd-logind.service
```


## 参考

1. 
