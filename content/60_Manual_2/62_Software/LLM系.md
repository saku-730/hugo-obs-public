---
title: LLM系
tags:
  - 2025/06
  - LLM
  - AI
created: 2025-06-08
updated: 2026-03-17
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# LLM系

企業が作った(汎用)LLMを使う上でのメモ。

## 全般的に

### 口調

デフォルトだと割と丁寧な喋り方が多い。しかし講義を受けているようでしんどくなってくるのでメモリやプロンプトでとにかくフランクな口調にする。ただしそのうち忘れて丁寧になってしまうことがあるのでそのときはまた口調を崩せよ、と言って壊し続ける。

LLMをギャルにしてバイブスをあげるとコーディング性能が上がるという話もあったりなかったり。

### プロンプト

してほしいではなく、何が不満か言ってみる。

## Gemini

Google作成。最近はバカと言われがち(2026-01)

### Gemini CLI

[GitHub - google-gemini/gemini-cli: An open-source AI agent that brings the power of Gemini directly into your terminal.](https://github.com/google-gemini/gemini-cli)

その時の新し目の[node_js]({{< relref "/50_Manual_1/51_Web/node_js" >}})がインストールされている必要がある。

インストール 
```sh
npm install -g @google/gemini-cli
```

[Gemini CLI のインストール方法と基本的な使い方](https://zenn.dev/torakm/articles/b844f29c9d349c)

[Obsidian x Gemini CLIで最強執筆環境を作ろう｜Naoki \|電電猫猫](https://note.com/electrical_cat/n/n5db5f038a391?sub_rt=share_pb)

```sh
gemini
```

で起動。`gemini.md`を作った上で指示を出すとそれをもとに作ってくれるのでなるべく作ること。

```sh
gemini --yoho
```

yohoモードだと権限の確認などを全部すっ飛ばしてどんどんファイル作成・編集などもしながら進んでいく。危ないモードだが楽でもある。ctrl + y で常にon/off 切り替えができる。心配なときは基本off でいけそうなときだけ on にするとか。

会話履歴 `/compress` で要約してそれを`/chat save <tag>`で保存。次同じプロジェクトをやるときは`/chat resume <tag>`で復元するのが良さそう。保存した会話はそのディレクトリで起動したときだけ復元できる。

作業が完了したことを教えないと永遠に過去のバグと戦い続けることがある。仮にそれがもう修正されていても何もないところでつまづき続けるのでそうなったら一回すべての作業が完了したと教える。

## ChatGPT

OpenAI作成。

会話しているとその内容を勝手にどんどん覚えていってくれる。パソコン環境とかを覚えてくれるのはいいが、勝手に早とちりしてしまうことも。

### Codex CLI

[Codex CLI](https://developers.openai.com/codex/cli)

ChatGPTのCLI版

インストール 参照[node_js]({{< relref "/50_Manual_1/51_Web/node_js" >}})

```bash
npm i -g @openai/codex
```

起動 初回は認証が必要。

```bash
codex
```


## 参考

1. [Gemini CLI コマンドリファレンス](https://zenn.dev/ideagarage/articles/2c7f4896b5fbe0)