---
title: Zotero
tags:
  - 2024/06
  - Zotero
  - Paper
created: 2024-06-01
updated: 2025-08-31
date: 2024-06-01
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Zotero

極める、使いこなす。

文献管理ソフトZoteroの使い方。

## インストール

[installation \[Zotero Documentation\]](https://www.zotero.org/support/installation)

### deb

```
wget -qO- https://raw.githubusercontent.com/retorquere/zotero-deb/master/install.sh | sudo bash
sudo apt update
sudo apt install zotero
```

割としっかりメンテナンスされている印象なのでaptでよさそう。

### tarball

ベータ版などはこれしか方法がない。ただそこまで難しくない。

公式サイトからダウンロードしたら解凍。それを``/usr/lib``におく。

実行ファイルのシンボリックリンクを作成
```
sudo ln -s /usr/lib/zotero-beta/zotero /usr/bin/zotero-beta
```

アプリケーションダッシュボードに表示するため``/usr/share/applications``に``.desktop``ファイルを追加。[MXLinux]({{< relref "/content/60_Manual_2/64_OS/MXLinux" >}}#アプリケーションダッシュボード-スタートメニュー)

## 設定

Edit ->Setting から 

Sync でアカウントにログインして同期する。これで論文のメタデータなどが同期されるが論文のpdf自体は同期されない。

論文pdfを同期するにはAdvancedのLinked Attachment Base Directoryを論文を保存しているディレクトリにする。

## コミュニティ

[Zotero | Get Involved](https://www.zotero.org/getinvolved)
ZoteroはOSSなのでコミュニティが文献管理ソフトにしては活発している。

## Plugin

### Translate

[GitHub - windingwind/zotero-pdf-translate: Translate PDF, EPub, webpage, metadata, annotations, notes to the target language. Support 20+ translate services.](https://github.com/windingwind/zotero-pdf-translate?tab=readme-ov-file)

外部の翻訳サービスを利用して論文を翻訳できる。

単語を選んだときは翻訳サービスではなく辞書サービスを使うことが可能。

翻訳サービスにDeepl、辞書サービスにWeblioを使用中。DeeplにはAPIキーが必要で無料は上限あるがかなり容量多め。


## 拡張機能

Chrome拡張機能が使える。論文のサイトにいってこの拡張機能で保存先を選べば自動でpdfをダウンロードしてくれる。従来ではpdfをダウンロードしてそれを文献管理ソフトに取り込むという操作が必要だったがこれでブラウザからクリックするだけでできるようになっていてすごくいい。

### Science Directでダウンロードできない問題

==version7から改善された。==

Science Directがbot対策をしたため上記の拡張機能が利用できなくなった。[Forumでも議論されており](https://forums.zotero.org/discussion/comment/451390/#Comment_451390)現在のリリース版のversion6では解決していないがbeta版のversion7では一応の解決をしている。

ただしこれでも人かどうかのポップアップがでてそれに回答する必要はある。

~~そのためbeta版に移行することにする。~~ →プラグインが利用できなかったのでひとまずversion6で拡張機能を我慢しながら使う。

