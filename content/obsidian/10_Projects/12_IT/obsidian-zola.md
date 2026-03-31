---
title: obsidian-zola
tags:
  - 2025/07
  - Git/GitHub
created: 2025-07-31
updated: 2026-03-17
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# obsidian-zola

Obsidianの記事をzolaで公開する。

## 要件

- Obsidianの表示を保ってzolaで公開する。
- 内部リンク構造やタグもそのまま保つ。
- ファイル構造も保つ。
- ディレクトリ・各マークダウンごとに公開、非公開を設定可能にする。
- obsidianのGithubリポジトリからzolaのGithubリポジトリに1日1回、変更反映のactionを行う。
- zolaのGithubリポジトリはobsidianからの変更反映Pushをされたらそれを起因にレンタルサーバーへPushする。
- トップページなど一部の特定ページはzolaの方で独自に作製する。

## Github action

1. obsidianについてローカルからgithubリポジトリにpush
2. 1日1回 obsidian リポジトリからaction実行
	1. obsidianのマークダウンをzola用に編集
	2. zolaのリポジトリと編集したマークダウンの差分更新
	3. 添付ファイルも差分更新
3. zolaリポジトリに更新があればzolaリポジトリからレンタルサーバーにgithub action
	1. zolaをビルド
	2. ビルド後のファイルを差分更新

## obsidian

## zola

## 進行状況

obs2zolaでmain.goとfrontmatter-convert.goでおおよそマークダウンファイルの書き換えはできてきているがまだ改善点あり。

- ファイル_indexを自動で作成した
- ↑トップページとかは独自に作りたい。今のままだと上書きされちゃうのでどうにか。
- main.goが膨らんできたので軽量化中。とりあえず動く。

### 次にやること

- フロントマターのタグとかが全く機能していない。
- 画像の内部リンクをうまくやる。
- 右サイドバーに見出しリンクとか
- draft を検知

## 参考

1. 