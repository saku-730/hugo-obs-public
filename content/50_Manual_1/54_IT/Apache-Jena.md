---
title: Apache-Jena
tags:
  - 2026/03
  - RDF
  - Linked-data
  - semantic-web
created: 2026-03-18
updated: 2026-05-21
draft: false
---
セマンティックwebとLinked Dataのためのフレームワーク。もっとわかりやすく言えば、RDFトリプルのデータベースソフト的な。

![](/attachments/Pasted%20image%2020260515134333.png)

[Apache Jena - Getting started with Apache Jena](https://jena.apache.org/getting_started/)より

一応、Apache jena は↑の図にある通り、RDF関係のフレームワーク、ライブラリを指すが、私が使うのはほとんど、Fusekiだけなのでそれについて。

## Fuseki install

[Central Repository: org/apache/jena/jena-fuseki-docker](https://repo1.maven.org/maven2/org/apache/jena/jena-fuseki-docker/)ここでdocker composeファイルを探す。基本は docker compose でやるなら↓のような感じ。なお、`command`のディレクトリ、`databases/occurrence`がないとエラーで落ちる。

[Apache Jena - Fuseki : Plain Server](https://jena.apache.org/documentation/fuseki2/fuseki-plain#fuseki-docker)参考

```yaml
  fuseki:
    build:
      context: .
      args:
        JENA_VERSION: 6.0.0
    container_name: occurrence_fuseki
    ports:
      - "3030:3030"
    volumes:
      - ./databases:/fuseki/databases
    command:
      - "--update"
      - "--loc"
      - "databases/occurrence"
      - "/occurrence"
```

dockerでやる場合、webUIがないので、もしwebUIを見たい場合には、直接ダウンロードして起動する。


## 参考

1. [Apache Jena - Apache Jena documentation overview](https://jena.apache.org/documentation/)
