---
title: "Obidian の使い方,設定メモ"
tags:
  - 2024/05
  - Note
  - Obsidian
created: 2024-05-30
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Obsidian の使い方,設定メモ

## 概要
Obidianの運用上、色々変更した設定や使い方をとりあえずメモしていくノート

そのうちきれいにまとめる。本(同人紙)にできたらなおよし。

## インストール

[Download - Obsidian](https://obsidian.md/download)より。snapは日本語入力ができない問題がある。
コミュニティ公式サポート的なのはFlatpakでこちらは今のところ問題がないのでFlatpakを推奨。debも問題はあまりないが安定感はFlatpakのほうがある気がする。

## 方針
- データはマークダウン形式でローカル(とクラウド)に保存されるので仮に、Obsidianが使えなくなってもマークダウンを他の方法でも使えるようにある程度の汎用性を持ったマークダウンを作成する。(Obsidian でしか使えないような記法は避ける)
- 楽に楽しく

## 設定編
- エディタ>デフォルト編集モード を"ソースコード" に設定。[1] 右半分をプレビューにするのでプレビューを編集モードで必要ないため。
- ディレクトリ構成は[Note 分類基準]({{< relref "/60_Manual_2/61_Notebook/Note 分類基準" >}})を参照
- エディタ>高度な設定 から入力を"vimモード"に設定する。
- Daily noteの設定は[手を動かして分かる、Obsidianの始め方 - shikixyx](https://shikixyx.hatenablog.com/entry/2023/03/24/101954)を参考にする。ただしDaile_noteのテンプレートの時間表示のみ24時間にするため 作成日: {{date:YYYY年MM月DD日（ddd）HH:mm}} に変更。
- 外観 > interface で「インラインタイトルの表示」をオフにする
- ~~右側のサイドパネルは使いたくない→右側サイドパネルのカレンダー,タブをクリック&ドロップで左側サイドパネルに移動させられる~~
- サイドバネルのメニューはドラッグで順番、位置を入れ替えられる。位置については左右、上下割と自由に移動できるがあたり判定が小さいので注意。
- 日本語フォントがデフォルトのは特に感じがおかしいので変える。settings > apparenceからフォントを変える。

### 目次作成
[ObsidianでもTOCしたい](https://ubanis.com/note/obsidian_toc/)
[Obsidianに見出しの目次を作るアクション - Jazzと読書の日々](https://wineroses.hatenablog.com/entry/2023/02/17/192457)

上2つの方法だと更新するたびに目次を作り直さないと行けない。動的に作成したいので↓のプラグインを利用。これでつくられる目次を折りたたむために目次をh6でつくりmaxLevel:5に設定。
minLevel:2で概要への目次はなくす。

[Automatic Table Of Contents](https://github.com/johansatge/obsidian-automatic-table-of-contents?tab=readme-ov-file)

### プラグイン

#### Tempater

[Templater](https://github.com/SilentVoid13/Templater)
テンプレートにjavascriptをつかえるようにして色々できるようにする。

#### Dataview

[Dataview](https://github.com/blacksmithgu/obsidian-dataview)
データのつながりとか。作成したノートの情報を持ってくるのに必要。
他の多くのプラグインがDaataviewに依存しており必須プラグインの一つ。

#### Auto Link Title

[Auto Link Title](https://github.com/zolrath/obsidian-auto-link-title)
urlを貼ると自動でwebタイトルのリンク形式にしてくれる。とりあえずリンク貼るときにきれいになるので便利。

#### Calender

[Calendar](https://github.com/liamcain/obsidian-calendar-plugin)
Daliry note をカレンダー形式で見れるようにする。デフォルトだと右サイドパネルにカレンダーが配置される。ドラッグ&ドロップで左サイドパネルに移動可能。

#### Automatic Table Of Contents

[Automatic Table Of Contents](https://github.com/johansatge/obsidian-automatic-table-of-contents?tab=readme-ov-file)
目次の自動作成。編集に応じて動的に目次を更新してくれるのであとから書き換えたりする必要が無い。テンプレートで目次を作ると後々、更新が必要になってしまう。

#### Update time on edit

[Update time on edit](https://github.com/beaussan/update-time-on-edit-obsidian)
作成、更新日時をプロパティに自動挿入。更新日時は設定で1分-から確認する時間を設定できる。テンプレートとDaily noteは除外している。自動更新は編集画面を切り替えると変わってる。

#### Tag-Wrangler

[Tag-Wrangler](https://github.com/pjeby/tag-wrangler)
タグ機能の追加。タグペインで右クリックしたときのメニューができる。主な用途はタグ名変更。

#### Obsidian Book Search Plugin

[obsidian-book-search-plugin](https://github.com/anpigon/obsidian-book-search-plugin?tab=readme-ov-file#template-variables-definitions)
書籍の題名またはISBNを使って検索を行いページを取得情報をもとに自動で作成する。書籍のデータベースはGoogle books api を使用している。テンプレートを設定することが可能でありobsidian-book-pluginがそれである。

#### Git

Github連携用。

### Github連携

[Github](https://github.com/saku-730/My-obsidian)

1. Github にリモートリポジトリを新規作成
2. ObsidianのコミュニティプラグインのGitをインストール、有効化
3. Obsidianのvalutディレクトリでgitを設定
```bash
git init
git remote add origin git@github.com:saku-730/My-obsidian.git
git add .
git commit -m 'first'
```
 Githubのリモートリポジトリに Obsidianのvaultがコピーされていればok
Obsidianの右サイドバーにGitプラグインが表示され、GUIでGithubの同期が可能になる。

[SSH]({{< relref "/60_Manual_2/62_Software/SSH" >}}#ssh-config)でgithubのsshを設定しておく。

すでにリポジトリを作っていて新たなパソコンなどにobsidianを導入する場合、

```sh
git clone git@github.com:saku-730/My-obsidian.git
```

↑でコピーした上でssh設定をする。httpsでcloneしてしまうと、ssh設定が生きないので注意。そうなると、いちいちgit push の際などにログイン認証を求められるので必ずsshで。

GitプラグインでPull on startupをON。Commit messageに{{hostname}}でデバイス名を追加。

Flatpakでインストールした場合、`.ssh`にアクセスできないことがあるので
```
flatpak override --filesystem=~/.ssh com.obsidian.Obsidian
```
で権限を付与する。

5分ごとに commit, push を行う設定にする。

## 使い方編

- 右上のモード変換をctrl押しながらクリックでプレビューを即展開。
- 右半分にプレビュー即時反映、左半分はソースコード[1]。左側にサイドパネルでディレクトリ等表示、右側サイドパネルの上側に見出し、下側にGitを表示。
- テンプレートはDaily note用とそれ以外の2種類用意。プロパティに作成日、更新日、タグは必須。title要素は一応入れておいた。作成日と更新日はプラグインのUpdate time on editに任せるのでテンプレートには入れない。入れると逆に無駄が増えてよくない。→Obsidian Book Search Plugin で使用するテンプレートを追加。
- タグ名は頭文字のみ大文字。複数単語はなるべく避け使用する場合は_でつなげる(スペース不可)。~~人名は田中 アンダーバー太郎」みたいにする。~~ → Obsidian Book Search Pluginによって取得する著者情報を基準に性名の間を空けない「田中太郎」のようにする。 タグ名変更等はを用いる。スネークケースの変化形みたいな。

## 記事の書き方

### フロントマター

タグはなるべく多く。きれいさよりも検索性を重視する。タグには自動で記事の作成月が付与される。created, updated はそれぞれ最初に記事を作成した日時と最終更新日時。拡張機能のUpdate time on edit で自動で編集されるのでいじらない。

Obsidian Book Search Plugin を使った場合には出版社等の情報が追加されるがデータベースから取得できない場合が多いので可能な範囲で追記する。

### 本文

見出しのレベルは飛ばさないこと。また最大のh1は記事の題名のみに使う。目次や読みやすさの観点からh5までには収めたい。

参考にした文献等は最後にh2 参考 にまとめる。数字順にすると出典を書くときにわかりやすいので数字リストにする。ネット記事は基本 Auto link title でつくられたリンクのままでいいが、qiitaなどで#が含まれてしまい、意図せずタグ挿入していることがあるので注意すること。

## 参考

各メモに添付しているものも参考にすること。
1. [Obsidian.Zenn](https://zenn.dev/estra/books/obsidian-dot-zenn) zennの無料本
2. [Obsidian｜使いかたとコツ（目次）- Qiita](https://qiita.com/hann-solo/items/ac8fa75394813e8adcf4)
3. [Obsidianで最適なPKM環境を考える](https://zenn.dev/game8_blog/articles/0e50c36cd63b98#%E3%81%AF%E3%81%98%E3%82%81%E3%81%AB)
