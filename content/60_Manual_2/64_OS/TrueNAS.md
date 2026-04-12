---
title: Truenas
tags:
  - 2025/06
  - NAS
  - ネットワーク
created: 2025-06-01
updated: 2026-04-12
---
[TrueNAS - 192.168.2.161](http://192.168.2.161/ui/dashboard)

truenas_adminがデフォルトルートユーザー

## ストレージ

基本的な流れはPool作成してDataset作成して、SMB共有設定をする。

### Pool作成

Storage > Create Pool

Name は基本的に(SSD/HDD)-(Size)-(ID)にしている。数字が先頭は不可。

### Dataset作成

Datasets > Add Dataset 

適当な名前をつける。 設定適宜する。データセットは容量の設定が無く、基本的に共有しながら使えるだけ使う感じになる。それだと困る場合、Quotasを設定することで容量の上限を決められる。

[Quotas \| TrueNAS Documentation Hub](https://www.truenas.com/docs/scale/datasets/quotas/)

Datasets > Dataset Space Management から編集する。


## Bootストレージ

基本的にSSDミラー構成にする。片肺になったら通知。

16GB(intel optane)での運用が制限付きで可能

16GBの場合、古いバージョンはすぐに消すこととNAS以外の機能を入れないこと。

System > Boot  からBoot環境が見れる。古いのがあれば削除すること。

Storage > Disks(右上) > boot-pool のssdを選択、でS.M.A.R.Tテストと結果を見れる。やばかったらまだ動いていても変えたほうがいいかも。

## ユーザー管理

Credentials > Users からユーザーの管理画面に入れる。

ユーザーを追加するときはSSHは許可しない。管理者権限を与えたい場合、EditからAuxiliary Groupsにbuiltin_administratorsとbuiltin_usersを入れる。

## 省電力設定

電気代を抑えるためのあれやこれや

### HDD周り

Storage > Disks から対象HDDを選んでEdit 

1. HDD Standby : 60 (60分触らないと回転停止)
2 Advanced Power Management : Level1Minimum power usage with Standby (一番消費電力が小さくなる設定)

## Apps

### 共通

基本的に、OSはIntel optane 16GBで余裕が無いので、追加したSSDにappsのシステムを置く。

システムの置き場所は Storage Configurationの部分でixVolumeで自動作成でいい。

### Nextcloud

#### Install

基本とりあえずデフォルトでいいのでパスワードなどを適宜埋める。

その上で、インストールが完了するとwebUIにアクセスできるが、↓のようになる。

![](/attachments/Pasted%20image%2020260312172309.png)

`config.php`でアクセス許可に関して、自身のipを追加する必要がある。[Installation wizard — Nextcloud latest Administration Manual latest documentation](https://docs.nextcloud.com/server/33/admin_manual/installation/installation_wizard.html#trusted-domains)

~~Apps > Workloads からnextcloudのシェルに入る。~~

~~`/config/config.php`を編集。ここでvimはおろか、viすらないので詰む。~~

![](/attachments/Pasted%20image%2020260312173259.png)

↑のHost部分(Nextcloud Configuration)を自身のipにしておけばいい。

#### settings

Storage Configurationでシステムと共有用のデータセットを選ぶ。

システムはこだわりが無いので、ixVolumeのデフォルト設定でいく。

ストレージ(データセット)追加 [1]を参照。

![](/attachments/Pasted%20image%2020260312174046.png)

![](/attachments/Pasted%20image%2020260312173947.png)

## 参考

1. [NextcloudにTrueNASの任意のローカルストレージ(Dataset)を追加する \| prtn-blog](https://prtn-life.com/blog/nextcloud-add-trunas-storage#toc4)
