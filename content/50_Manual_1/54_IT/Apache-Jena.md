---
title: Apache-Jena
tags:
  - 2026/03
  - RDF
  - Linked-data
  - semantic-web
created: 2026-03-18
updated: 2026-07-22
draft: false
---
セマンティックwebとLinked Dataのためのフレームワーク。もっとわかりやすく言えば、RDFトリプルのデータベースソフト的なもの。ただし、フレームワークというだけあって、データベースよりもより広い範囲を含む。

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

## 設定

Fuseki では設定はconfigurationファイルを指定することで行います。

### configuration ファイルの書き方

設定ファイルの書き方はRDFグラフの書き方と同一です。読みやすさのため、turtleでの形式がいいと思います。

一つの設定ファイルに全て書き込みます。

[jena/jena-fuseki2/examples at main · apache/jena · GitHub](https://github.com/apache/jena/tree/main/jena-fuseki2/examples)

↓例

```turtle
## Licensed under the terms of http://www.apache.org/licenses/LICENSE-2.0

PREFIX :        <#>
PREFIX fuseki:  <http://jena.apache.org/fuseki#>
PREFIX rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs:    <http://www.w3.org/2000/01/rdf-schema#>
PREFIX ja:      <http://jena.hpl.hp.com/2005/11/Assembler#>

[] rdf:type fuseki:Server ;
   fuseki:services (
     :service
   ) .

## Service description for "/dataset" with all endpoints.
## e.g.
##   GET /dataset/query?query=...
##   GET /dataset/get?default (SPARQL Graph Store Protocol)

:service rdf:type fuseki:Service ;
    fuseki:name "dataset" ;

    ## The  GET /dataset?query= variants
    fuseki:endpoint [ fuseki:operation fuseki:query ; ] ;
    ## gsp-rw covers gsp-r and upload.
    fuseki:endpoint [ fuseki:operation fuseki:update ; ] ;
    fuseki:endpoint [ fuseki:operation fuseki:gsp-rw ; ] ;
    ## RDF Patch
    fuseki:endpoint [ fuseki:operation fuseki:patch ; ] ;

    fuseki:endpoint [ 
        fuseki:operation fuseki:query ;
        fuseki:name "sparql" 
    ];
    fuseki:endpoint [
        fuseki:operation fuseki:query ;
        fuseki:name "query" 
    ] ;
    fuseki:endpoint [
        fuseki:operation fuseki:update ;
        fuseki:name "update"
    ] ;
    fuseki:endpoint [
        fuseki:operation fuseki:gsp-r ;
        fuseki:name "get"
    ] ;
    fuseki:endpoint [ 
        fuseki:operation fuseki:gsp-rw ; 
        fuseki:name "data"
    ] ; 
    fuseki:endpoint [
        ## RDF Patch
        fuseki:operation fuseki:patch ;
        fuseki:name "patch"
    ] ; 
    fuseki:dataset :dataset ;
    .

# Transactional in-memory dataset.
:dataset rdf:type ja:MemoryDataset ;
    ## Optional load with data on start-up
    ## ja:data "data1.trig";
    ## ja:data "data2.trig";
    .
   
```
#### Prefix

省略のためのPrefix。主に使うのは次のもの。

```turtle
PREFIX fuseki:  <http://jena.apache.org/fuseki#>
PREFIX rdf:     <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
PREFIX rdfs:    <http://www.w3.org/2000/01/rdf-schema#>
PREFIX tdb2:    <http://jena.apache.org/2016/tdb#>
PREFIX tdb1:    <http://jena.hpl.hp.com/2008/tdb#>
PREFIX ja:      <http://jena.hpl.hp.com/2005/11/Assembler#>
PREFIX :        <#>
```

#### Server section

```turtle
[] rdf:type fuseki:Server ;
   fuseki:services (
     :service
   ) .
```

グローバルパラメータなど、サーバー全体に及ぶ設定を書きたいときにここに書く。このserver sectionは必須ではない。存在しない場合は、`fuseki:Service`をサーバーが検索してFusekiが構成される。
後述する、serviceが複数存在し、かつ選択的に公開したい場合には、公開するサーバーだけを次のように選択する。

```turtle
[] rdf:type fuseki:Server ;
   fuseki:services (
     :serviceA
     :serviceB
   ) .
   -------------
   :serviceA rdf:type fuseki:Service ;
    fuseki:name "a" ;
    fuseki:dataset :datasetA ;
    .

:serviceB rdf:type fuseki:Service ;
    fuseki:name "b" ;
    fuseki:dataset :datasetB ;
    .
```

server sectionは一つの設定ファイルに一つしか書けない。

最小の書き方は↓

```turtle
[] rdf:type fuseki:Server .
```

```turtle
[] a fuseki:Server .
```

2つは同じ意味になる。(Prefixでrdf:, fuseki:, は定義済みと想定)

先頭の[]はblank nodeで匿名のノードである。意味としては`この設定ファイルには、サーバー設定の匿名ノードがあるよ`になる。このノード自体は他で使うことがないので、基本的にblank node でいい。

次に↓の部分は公開するサービスについて選択する。ここで選択しなければそのサービスは公開されない。サービスが具体的に何を表すのかは後述。おおよそ、公開単位の一つくらいに考えて貰えればok。最初は一つしか作らないと思うので、これでいこう。

```turtle
   fuseki:services (
     :service
   ) .
```

以下、その他の些末な設定たち

##### サーバー全体のタイムアウト設定

```turtle
[] rdf:type fuseki:Server ;  
	ja:context [  
	ja:cxtName "arq:queryTimeout" ;  
	ja:cxtValue "10000, 60000"  
	] .
```

クエリのタイムアウト時間を設定する。単位はミリ秒で1000=1秒。 `10000,60000`は最初のクエリタイムアウトが10秒、全体で60秒。`10000`だけなら、単純に、全体クエリのタイムアウトが10秒。

後述のサービス内にも同様に、クエリのタイムアウトなどの各種設定、contextは追加可能で、その場合、上書きされる。優先度は server section < dataset の追加設定 < endpointの追加設定 の順になっている。

##### SPARQL UPDATEのタイムアウト設定

```turtle
[] rdf:type fuseki:Server ;
    ja:context [
        ja:cxtName "arq:updateTimeout" ;
        ja:cxtValue "60000"
    ] .
```

SPARQLのUPDATE処理でのタイムアウトの設定。サーバークエリのタイムアウト設定と書き方は同じ。`cxtName`だけ変える。

##### Access Control List (ACL)

```turtle
[] rdf:type fuseki:Server ;
    fuseki:allowedUsers "user1", "user2", "user3" ;
    fuseki:services (
        <#service>
    ) .
```

特定のサービスに対してアクセス可能なユーザーを設定できる。次のようにいくつかの形式があり、混合することも可能。

```turtle
fuseki:allowedUsers "user1", "user2", "user3" ;

fuseki:allowedUsers "user1" ;
fuseki:allowedUsers "user2" ;
fuseki:allowedUsers "user3" ;

fuseki:allowedUsers ( "user1" "user2" "user3" ) ;
```

[Apache Jena - Data Access Control for Fuseki](https://jena.apache.org/documentation/fuseki2/fuseki-data-access-control.html)

ACLもタイムアウト同様に、エンドポイント/サービスなどにもかける。その場合は、すべての段階で許可されているユーザーがそのエンドポイント/サービスをアクセス可能になる。

そのため、複数段階のACLを組み合わせることで、権限の段階的な付与が可能になっている。

ユーザー自体は次のpassword設定ファイルに書き込むことで作成する。

##### password

```turtle
[]] rdf:type fuseki:Server ;
    fuseki:passwd "users.passwd" ;
    fuseki:auth "digest" ;
    fuseki:allowedUsers "*" ;
    fuseki:services (
        <#service>
    ) .
```

users.passwd というパスワードファイルを使う、認証方式は digestである、認証済みユーザーは全員アクセス可能という意味。認証方式に関してはdigestかbasicがある。httpの認証フレームワークですが、基本パスワードがハッシュ化されることなどから、digestがいいかと。デフォルト設定もdigestです。

users.passwdの書き方は平文なら以下の通り

```text
backend: secret-password
admin: admin-password
```

ファイルを使えるようにするのは後述のconfiguration ファイルの使い方 で。

[Apache Jena - Data Access Control for Fuseki](https://jena.apache.org/documentation/fuseki2/fuseki-data-access-control.html)

#### Service

serviceとはurl上で公開するときの一つのまとまりを表す。例えばserviceAとserviceBをそれぞれ設定した場合、それぞれのアクセスurlは`http://fuseki:3030/serviceA`, `http://fuseki:3030/serviceB`となる。それぞれにデータセットやエンドポイントを設定できるので分けたいときにはサービスを複数作る。同じデータセットなら分ける必要がないことも多く、その場合はサービスは一つでいい。

```turtle
:service rdf:type fuseki:Service ;
    fuseki:name "occurrence" ;
    fuseki:endpoint [
        fuseki:operation fuseki:query ;
        fuseki:name "sparql"
    ] ;
    fuseki:dataset :dataset ;
    .
```

```turtle
PREFIX :        <#>
```

↑をPREFIXで定義しているので一行目：service は<#service>の意味。<#サービス名>
`rdf:type fuseki:Service`でfusekiでのserviceであることを定義する。

続いて、`fuseki:name`でurlでのserviceがどうなるのかを指定する。この例だと、`http://fuseki:3030/occurrence`みたいになる。サービス名はあくまで内部での取り扱いに使うだけでurlは別でここで指定する。

その次に`fuseki:endpoint`を指定する。これはAPIのエンドポイントの指定。例だと一つだけだが、必要に応じていくつも設定する。ただし、セキュリティ的には、無闇に設定せず、最低限にとどめておくのがよい。詳しくは次。

`fuseki:dataset`で使うデータセットを指定する。これはサービス一つに対して一つのみ指定する。この例では`:dataset`つまり`<#dataset>`でこれは最後の方のデータセット設定でより詳しく、どのディレクトリを使うか、どの種類化などを決める。ここではとりあえずこの名前だけ指定しておくでいい。

---
細かい話 `#`の意味

<#service>とするとserviceを一つ定義し始めているが、ここで`#`が必要な理由。これはフラグメント付きの相対IRIである必要があるから。

`#`がついてフラグメント付き相対IRIになると例えばbaseIRIが`file:///fuseki/config/config.ttl`のとき、<#service>は`file:///fuseki/config/config.ttl#service`になる。`#`なしの`<service>`は`file:///fuseki/config/service`になることがある。

ここでbaseIRIが何なんだよって話になるが、指定していなければ、基本的に設定ファイルの取得元になる。ここではファイルのパスになる。

`#`有り無しが混ざるのは指すパスが異なるのでだめだが、`<service>`で統一するは書き方的には間違いとも言えない。ただし、`file:///fuseki/config/config.ttl#service`って意味のほうが、設定ファイルの中の部品って言う感じがして収まりがいい。また公式の書き方的にも`<#service>`なのでおとなしく従っておこう。

なお、Turtleで`<>`はIRIになる。リテラルの場合は`""`

---

##### 各エンドポイント

[Apache Jena - Fuseki Data Service Configuration Syntax](https://jena.apache.org/documentation/fuseki2/fuseki-config-endpoint.html)

- SPARQL Query

```turtle
fuseki:endpoint [
    fuseki:operation fuseki:query ;
    fuseki:name "sparql"
] ;
```

URL`/service/sparql`

SPARQLのクエリ操作。Update以外のSELECT, CONSTRUCT, ASK, DESCRIBEなど。

- SPARQL Update

```turtle
fuseki:endpoint [
    fuseki:operation fuseki:update ;
    fuseki:name "update"
] ;
```

URL`/service/update`

RDFデータの更新をするSPARQL操作。

- Graph Store Protocol read only

```turtle
fuseki:endpoint [
    fuseki:operation fuseki:gsp_r ;
    fuseki:name "get"
] ;
```

RDFグラフの読み取り専用。更新を絶対にしない、読み取り口として使おう。

- Grapht Store Protocol

```turtle
fuseki:endpoint [
    fuseki:operation fuseki:gsp_rw ;
    fuseki:name "data"
] ;
```

RDFグラフの読み取り、書き込み。N-QuadsやTriGなどの形式で投入するなら、SPARQLではなくこっちを使う。

- SHACL

```turtle
fuseki:endpoint [
    fuseki:operation fuseki:shacl ;
    fuseki:name "shacl"
] ;
```

SHACL用。データの検証をする。

[Apache Jena - Apache Jena SHACL](https://jena.apache.org/documentation/shacl/#integration-with-apache-jena-fuseki)

- Upload

```turtle
fuseki:endpoint [  
	fuseki:operation fuseki:upload ;  
	fuseki:name "upload"  
] ;
```

htmlフォームからデータをuploadする用。フロントエンドから直接送る場合など。

#### dataset

```turtle
:DatasetA rdf:type tdb2:DatasetTDB2 ;  
	tdb2:location "/fuseki/databases/datasetA" ;  
	.
```

Serviceの最後のほうで決めていた、使うデータセットについて、具体的な仕様をここで決めていく。基本の書き方は上に示したとおりで、データセット名を最初に示し、その後、データセットの種類を`rdf:type`で指定する。

2行目は同じ主語を使いまわすので省略で、具体的なデータセットのパスを指定する。この部分がdockerならvolumeに含まれて使えるようになっている必要がある。

```turtle
:dataset rdf:type tdb2:DatasetTDB2 ;  
	tdb2:location "/fuseki/databases/occurrence" ;  
		ja:context [  
			ja:cxtName "arq:queryTimeout" ;  
			ja:cxtValue "10000,60000"  
	] ;  
.
```

こんな感じでdatasetごとにクエリタイムアウトなどを設定することもできる。これはserviceの次に優先される。

#### Assembler

オブジェクトを構築するものです。ここでいう、オブジェクトとは、データセットやオントロジーなどを指します。つまり、オブジェクトとそれをどのように実装するかを決めているのが、Assemblerです。

AssemblerもRDFグラフ形式、多くはturtleで書きます。

dataset / model / graph section について記述する部分。

```turtle
:名前 rdf:type 作りたいオブジェクトの型 ;
    必要な設定プロパティ 値 ;
    .
```

基本の書き方。datasetはAssemblerの一種といえる。

[Apache Jena - Jena assembler quickstart](https://jena.apache.org/documentation/assembler/index.html)

[Apache Jena - Inside assemblers](https://jena.apache.org/documentation/assembler/inside-assemblers.html)

### configuration ファイルの使い方

#### Docker

```yaml
services:  
	fuseki:  
		build:  
			context: ./jena-fuseki-docker-6.1.0  
			dockerfile: Dockerfile  
			args:  
				JENA_VERSION: 6.0.0  
	container_name: occurrence_fuseki  
	volumes:  
		- ./fuseki/config/config.ttl:/fuseki/config/config.ttl:ro  
		- ./fuseki/config/users.passwd:/fuseki/config/users.passwd:ro  
		- ./fuseki/databases:/fuseki/databases  
	command:  
		- "--conf"  
		- "/fuseki/config/config.ttl"
```

ここでは、volumesに設定ファイルの`config.ttl`と`users.passwd`を入れて、コマンドで指定している。`config.ttl`の中で`users.passwd`を指定している想定。

こうやらずに、全部コマンドでやるのもできなくはない。

```yaml
command:  
	- "--passwd=/fuseki/config/users.passwd"  
	- "--auth=basic"  
	- "--tdb2"  
	- "--loc"
```

#### 直にインストールの場合

```text
apache-jena-fuseki-6.x.x/  
	config/  
		config.ttl  
		users.passwd  
	databases/  
		occurrence/
```

↑みたいなディレクトリ配置にして`./fuseki-server --conf config/config.ttl`とする。設定ファイルなしなら↓

```text
./fuseki-server \
	  --passwd=config/users.passwd \
	  --auth=basic \
	  --tdb2 \
	  --loc databases/occurrence \
	  --update \
	  /**occurrence**
```

上のどっちかになる。

[Apache Jena - Fuseki Data Service Configuration Syntax](https://jena.apache.org/documentation/fuseki2/fuseki-config-endpoint.html)

## Command for Jena 

いくつか、サーバーコマンドがある。使用機会はあまり多くないかもしれないが、これでしかできないようなこともあったりするので使える用にしておこう。なお、dockerではそのままでは使えないので注意。

[Apache Jena - Command-line and other tools for Jena developers](https://jena.apache.org/documentation/tools/)

## Docker での使い方・注意点

公式がdockerfileを提供しているので、これを使う。

注意点として

> The docker container is based on [Fuseki main](https://jena.apache.org/documentation/fuseki2/fuseki-main) for running a SPARQL server.

[Apache Jena - Fuseki : Docker Tools](https://jena.apache.org/documentation/fuseki2/fuseki-docker.html)

とあるとおり、SPARQLサーバーとしての運用を想定されているので、システムインストールであったいろいろな機能が省かれている。

1. GUI

システムインストールでは、WebGUIが備わっており、SPARQLをそこで試したりデータベースの概要を把握できたり、簡単なデータベース操作もできたが、その機能がまるごと無い。

基本的にコマンドラインでの運用となる。

2. Jena CLI

[Apache Jena - Command-line and other tools for Jena developers](https://jena.apache.org/documentation/tools/)

```
ARG JENA_VERSION=6.1.0

ENV JENA_HOME=/opt/jena
ENV PATH="${JENA_HOME}/bin:${PATH}"

RUN apt-get update \
    && apt-get install -y --no-install-recommends curl ca-certificates tar \
    && curl -fSL "https://archive.apache.org/dist/jena/binaries/apache-jena-${JENA_VERSION}.tar.gz" -o /tmp/apache-jena.tar.gz \
    && tar -xzf /tmp/apache-jena.tar.gz -C /opt \
    && ln -s "/opt/apache-jena-${JENA_VERSION}" "${JENA_HOME}" \
    && rm /tmp/apache-jena.tar.gz \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*
```


## 参考

1. [Apache Jena - Apache Jena documentation overview](https://jena.apache.org/documentation/)
