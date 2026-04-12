---
title: Go
tags:
  - 2024/11
  - Go
created: 2024-11-03
updated: 2026-04-12
---
検索するときはGolangとかね。

## install

バージョンについては新しくなったらまた入れること。自動更新ではない。Goを複数バージョンインストールすると実行時は一番最近、いれたGoを使う。ただ公式の↓を見る限り毎回すでに入っているGoは消すっていう考え方らしい。一応、複数バージョン入れても使える。よっぽどのことがない限りそのときの一番新しいstable versionsでいい。[All releases - The Go Programming Language](https://go.dev/dl/)
```
 rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go1.23.2.linux-amd64.tar.gz
```

インストールは↑のコマンドだけで終わる。パスを次のコマンドで通す。
```
export PATH=$PATH:/usr/local/go/bin
go version
```

↑で大丈夫だったら.bashrcに書き込もう。

```sh
echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc
source ~/.bashrc
```

## 基本コマンド

参考3にすべて書いてある。

ファイル実行。コンパイルしてそれを実行する。コンパイルしたファイルは残らない。インタープリター言語みたいに使える。

```bash
go run main.go
```

```bash
go run .
```

↑の書き方なら自動でmain.goを探してコンパイル、実行する。main.go以外をimportしているときはこっちじゃないとだめなのでこっちを基本と考えてもよし。

コンパイル。ファイル名をしてしなければmainになる。
```
go build main.go -o filename
```

## パッケージ

基本的に一つのプロジェクトは一つのディレクトリ内に作成するという方針である。

###  GOPATH

`/usr/loca/go/src`に内部パッケージが存在しておりそれらは`import <パッケージ名>`でimport できる。`/usr/loca/go/src`をGOPATHとよぶ。内部パッケージはこの仕組みで使う。

ユーザーが追加ダウンロードしたライブラリは`go env GOPATH`に存在する。

### moduleモード

Go 1.11以降導入された。

```go
go mod init <モジュール名>
```
でそのプロジェクトのモジュール情報をモジュール名で初期化。最初にこれをやる。

これによって`go.mod`ファイルがそのプロジェクトのディレクトリに作成される。go.modの役割としてはモジュール名と使用しているGoのバージョン、ライブラリの記録である。ライブラリを新たにインストールすると自動で追記されていく。

```go
go mod tidy
```
これでライブラリを整理してくれる。ソースコード中でimportされているものがダウンロードされていなければダウンロードしようとする。反対に一度もimportされていないのに`go.mod`に記述されている場合、その部分を削除する。とりあえずやっておけ。


## 基本の書き方

```go
pacake パッケージ名

import (
	パッケージ
)

func main (引数)戻り値{
	処理とか色々
}

```

`package`で最初にパッケージ名を宣言する。メインプログラムのパッケージ名は必ず`main`になる。

`import`でライブラリを読み込む。パッケージ名を記述する。

`func main` main という関数で処理を定義する。

### 書式

- インデントはタブ
- 演算子の前後は詰める。スペースなし。 1+1
- 

### 関数

#### 組み込み関数

- Println(値) : 改行して出力
- Print(値) : 改行せずに出力

#### 定義

```go
func main(){

}
```

### 制御構文

#### if

#### switch

#### for

### 構造体

### インターフェース

<目的>

構造体に必要なメソッドが必ず用意されていることを保証する。

<実装>



## 参考

1. [The Go Programming Language](https://go.dev)
2. [Go言語ハンズオン]({{% relref "/30_Reading_record/33_Computer/Go言語ハンズオン" %}})
3. [go command - cmd/go - Go Packages](https://pkg.go.dev/cmd/go)
