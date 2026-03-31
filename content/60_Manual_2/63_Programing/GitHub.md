---
title: GitHub
tags:
  - 2025/08
created: 2025-08-05
updated: 2025-08-31
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# GitHub

## GitHub Action

一時的にGithubの仮想マシン上でシェルスクリプトを走らせてサービスのデプロイをしたり更新を自動化したりできる。

### Git コマンド

Github action上で`git pull`などのgitコマンドを行う場合の注意点

最初に設定をする必要がある。参考[2][3]

```bash
git config user.name "github-actions[bot]" 
git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
```


## 参考

1. [GitHub Actionsの基本まとめ GitHubActions - Qiita](https://qiita.com/fukuidaito/items/9263a1da9db4015c3a65)
2. [GitHub Actions中でpushする際にgithub-actions\[bot\]をユーザーとして使う](https://rcmdnk.com/blog/2022/09/29/computer-github/)
3. [GitHub Push · Actions · GitHub Marketplace · GitHub](https://github.com/marketplace/actions/github-push)