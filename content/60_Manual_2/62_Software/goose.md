---
title: goose
tags:
  - 2025/12
  - Go
created: 2025-12-18
updated: 2026-03-17
draft: false
---
## install

```bash
go install github.com/pressly/goose/v3/cmd/goose@latest
```

go 1.21以上のインストールが必要。

パスを通す

```bash
export PATH="$(go env GOPATH)/bin:$PATH"
hash -r
which goose
goose -version
```

```bash
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.bashrc
echo 'export PATH="$(go env GOPATH)/bin:$PATH"' >> ~/.profile

source ~/.bashrc
which goose
goose -version
```

## マイグレーション

## 参考

1. 
