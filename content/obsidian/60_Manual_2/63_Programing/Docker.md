---
title: Docker
tags:
  - 2025/10
created: 2025-10-09
updated: 2026-03-17
draft: false
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# Docker

## Install

[Ubuntu \| Docker Docs](https://docs.docker.com/engine/install/ubuntu/)

↑公式に従え

既存のものを消去　あるかわからなければとりあえず実行しておけ。

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

リポジトリ登録

```bash
# Add Docker's official GPG key:
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "${UBUNTU_CODENAME:-$VERSION_CODENAME}") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

インストール

```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

hello worldで確認

```bash
sudo docker run hello-world
```

## 参考

1. 