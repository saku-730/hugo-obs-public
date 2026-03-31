---
title: ibm_V1
tags:
  - 2024/06
  - Individual_based_model
created: 2024-06-08
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# ibm_V1

ミミズ繁殖のIndividual Based Model をつくる。

## 目的

ミミズの繁殖をシミュレーションする。

==仮説：ミミズの一個体繁殖は繁殖干渉と交尾における切断リスク回避が要因。==

## 準備 情報集め

ibm,abmを使用した論文を読む。生物系に限らない。集計は[ibm]({{< relref "20_Research/23_Theory/ibm.md" >}})で行う。

## 設計

個体が自由に移動できるような2次元ibm。その過程で繁殖を行い子孫を残す。

- 