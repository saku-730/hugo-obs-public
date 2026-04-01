---
title: Git
tags:
  - 2024/06
  - Git
  - Git/GitHub
created: 2024-06-04
updated: 2025-08-31
aliases:
  - git
  - github
---
Linus がつくった履歴管理の定番。

## 運用メモ

- rebaseは特に気にならなければ行わない。rebaseして履歴が変わるデメリットのほうが大きく感じる。
- 脳死で最初にpullして環境を合わせる。
- httpsよりsshを使ったほうが認証が楽。

## 作業フロー

1. Github にリポジトリをつくる。[saku-730 (saku-730) / Repositories · GitHub](https://github.com/saku-730?tab=repositories)
2. プロジェクトのディレクトリをつくる。
3. ```bash
git clone <URL.git>
4. 作業用ディレクトリができたので後はpull,push
5. main ブランチは常にデプロイ可能なものにして適宜、ブランチを作成

## 基本コマンド

リモートリポジトリの追加。後々のことを考えてSSHにしよう。
```bash
git remote add origin <URL>
```

リモートリポジトリの削除
```bash
git remote remove origin
```

リモートリポジトリ一覧の表示。
```bash
git remote -v
```

アップストリームブランチの設定。
```bash
git push --set-upstream origin main
```

ブランチの作成とブランチの切り替え

```bash
git checkout -b <branch name>
```

## コミットメッセージ

毎回考えるのは無駄が多い。整理されていないメッセージは読みづらい。
→書き方にルールを設けるべき。フォーマットをつくる。

参考
- [Gitのコミットメッセージの書き方（2023年ver.）](https://zenn.dev/itosho/articles/git-commit-message-2023)


## Git flow

Gitの流れ。メインのブランチを必ず一つ作り常に使える(公開できる)ものがどれかはっきりさせる。バグ修正、新機能追加はそれぞれ新しいブランチ(トピックブランチ)を作り完了次第、mergeさせる。Git Hub Flow を主に参考にしていく。

 
### メインブランチ

#### main

一番メインとなるブランチ。これからブランチを作成しこれにマージさせる形で進めていく。軸となる一つの枝。

### トピックブランチ

それぞれの用途別に名前をつけて作成し、終わり次第mainにmergeする。基本的な名前は以下の通り。

- bug_fix バグ修正
- ***-feature ***の機能の追加

## 仕組み

`/objects`内のディレクトリ名はhash値の前2文字。その中のファイル名はそれに続く38文字。`/objects`ディレクトリがデータベースになっていてそれぞれのファイルはblobなどを指す。



## 小話

### mainとmaster

Gitのデフォルトブランチ名がmasterだったが奴隷とかのイメージであまり良くないということで2020?くらいにGitがmainにデフォルトを変えた。そのため基本的にはデフォルトのメインブランチ名はmainで使っていく。ただ昔から続いているプロジェクトとかだとまだmasterがメインブランチ名だったりするので注意。

## 参考
- [GitHub Flow (Japanese translation) · GitHub](https://gist.github.com/Gab-km/3705015)
- [A successful Git branching model » nvie.com](https://nvie.com/posts/a-successful-git-branching-model/)
-
