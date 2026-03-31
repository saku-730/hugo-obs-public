---
title: Kali
tags:
  - 2026/01
created: 2026-01-07
updated: 2026-03-17
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Kali

## 基本情報

- 必要ディスク容量：64GB以上 できれば128GB以上

## メモ

- vivaldiが安定しない

## 追加ソフトウェア

### パッケージ関係

#### snap

[Installing snapd on Kali Linux \| Kali Linux Documentation](https://www.kali.org/docs/tools/snap/)

インストール

```zsh
sudo apt update
sudo apt install snapd
```

すぐに有効化

```zsh
sudo systemctl enable --now snapd apparmor
```

snapのパスを通す
```zsh
export PATH=$PATH:/snap/bin
```

## 参考

1. 