---
title: ComfyUI
tags:
  - 2026/02
  - ComfyUI
  - 画像生成
created: 2026-02-01
updated: 2026-03-17
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# ComfyUI

## モデルプラットフォーム

### CIVIT AI

一番使うことになるであろう、AIモデルや画像の共有プラットフォーム

CLIでのダウンロード方法は↓

```bash
wget --content-disposition  "https://civitai.com/api/download/models/1234567
```

最後の1234567はURLの`VersionId=`の部分。

## ワークフロー

### CheckPoint

[WAI-illustrious-SDXL - v16.0 \| Illustrious Checkpoint \| Civitai](https://civitai.com/models/827184?modelVersionId=2514310)

### CLIPテキストエンコード プロンプト

### VAE

変分自己符号化器（Variational Auto-Encoder）

> とにかく**AIにしかわからない画像を人間に分かるように変換するときのAIモデルだ。**
[2] より




## 参考

1. [ComfyUI ウィキ チュートリアル マニュアル \| ComfyUI Wiki](https://comfyui-wiki.com/ja)
2. [【ComfyUI基礎シリーズ#5】VAEを覚えよう \| 謎の技術研究部](https://www.ultra-noob.com/blog/2023/44/)