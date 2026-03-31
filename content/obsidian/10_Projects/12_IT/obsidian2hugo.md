---
title: obsidian2hugo
tags:
  - Git/GitHub
  - 2026/03
created: 2026-03-31
updated: 2026-03-31
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# obsidian2hugo

## 参考

1. 

Obsidianの記事をhugoで公開する。

## 要件

- Obsidianの内容をそのまま改変せずにhugoで公開する。
- 内部リンク構造やタグもそのまま保つ。
- ファイル構造も保つ。
- ディレクトリ・各マークダウンごとに公開、非公開を設定可能にする。
- 各マークダウンファイルに、フロントマターでdraftがあればそれに応じて公開、非公開をする。なければ公開。
- obsidianのGithubリポジトリからhugoのGithubリポジトリに1日1回、変更反映のactionを行う。
- hugoのGithubリポジトリはobsidianからの変更反映Pushをされたらそれを起因に静的サイトホスティングサービスが更新。
- トップページなど一部の特定ページはhugoの方で独自に作製する。

関係するgithubリポジトリは3つ。

1. Obsidianリポジトリ：obsidianのコンテンツ、添付ファイル等がすべて格納されている。
2. hugoリポジトリ：obsidianのコンテンツがhugo用に変更されたものをコンテンツとして持ち、サイトを構築していて、ホスティングサービスが公開するのに使う。
3. obs2hugoリポジトリ ： 1日1回のgithub actionを行うことでobsidianリポジトリの内容を、hugoリポジトリに反映する。

## Github action

1. obsidianのgithubリポジトリを1日1回、obs2hugoリポジトリに一時読み込みする。
2. マークダウンの変換を行い、その内容を別ディレクトリに保管。
3. 変換後の内容を元に、hugoリポジトリを差分更新する。


## obsidian

## hugo

## 進行状況

- 2026-03-31: Go 製 CLI の初期実装を追加。Obsidian リポジトリを走査し、Markdown は Hugo の `content` 配下、添付ファイルは `static` 配下へ同期する構成にした。
- 2026-03-31: `Wiki Link` を Hugo の `relref` 形式へ変換し、`![](/obsidian/image.png)` などの添付参照を Hugo の静的 URL に変換する処理を追加。
- 2026-03-31: Obsidian 側ルートに `.obs2hugo.yaml` を置く前提で、`draft_paths` と `exclude_paths` による公開制御を実装。
- 2026-03-31: `.github/workflows/sync.yml` を追加。obs2hugo リポジトリを起点に Obsidian/Hugo の両リポジトリを checkout して定期同期する形にした。
- 2026-03-31: Hugo 側の独自ページを壊さないように、生成先は `content/obsidian` と `static/obsidian` のような専用管理ディレクトリに限定する方針にした。

## 実装メモ

- 変換処理は `go run ./cmd/obs2hugo sync` で実行する。
- Hugo 側の `content-dir` と `static-dir` は毎回作り直すため、obs2hugo が管理する専用ディレクトリを使う。
- Markdown の front matter は簡易 YAML パーサで処理する。現段階ではトップレベルの scalar と配列を対象にする。
- Obsidian のノート名リンクは、同名ファイルが一意に解決できる場合のみ basename からリンク解決する。
- 同名ノートが複数あるケースや、複雑な埋め込み構文は今後の拡張対象。

## 参考

1. 
