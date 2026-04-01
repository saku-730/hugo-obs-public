---
title: R
tags:
  - 2025/03
  - R
  - Rstudio
created: 2025-03-05
updated: 2025-08-31
---
## インストール

[The Comprehensive R Archive Network](https://ftp.yz.yamagata-u.ac.jp/pub/cran/)


```bash
sudo apt update -qq
sudo apt install --no-install-recommends software-properties-common dirmngr
wget -qO- https://cloud.r-project.org/bin/linux/ubuntu/marutter_pubkey.asc | sudo tee -a /etc/apt/trusted.gpg.d/cran_ubuntu_key.asc
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
sudo add-apt-repository "deb https://cloud.r-project.org/bin/linux/ubuntu $(lsb_release -cs)-cran40/"
sudo apt-get install r-base-dev
```

Rstudio インストール

[RStudio Desktop - Posit](https://posit.co/download/rstudio-desktop/)

## パッケージ

tidyverseで必要なライブラリをインストールする。

```bash
sudo apt install libxml2-dev libfontconfig1-dev libcurl4-openssl-dev  libcurl4-openssl-dev libharfbuzz-dev libfribidi-dev libfreetype6-dev libpng-dev libtiff5-dev libjpeg-dev
```

[Tidyverse](https://www.tidyverse.org)


## 書き方

### 基本

最初に環境変数をすべてリセットする。

```R
rm(list=objects())
```



## RStudio

### 設定

Tools > Global options(一番下) から色々変えられる。

とりあえず変えたほうがいいのは

- Appearance Editor themeをTomorrow Night Brightに
- Pane Layout Add ColumnでSourceを追加
- Packages からPrimary CRAN repository: をJapan(山形大学)に変更
- Code Editing>Keybindings: からVimに変更

## RStudio Server

Rstudio serever インストール

[RStudio Server - Posit](https://posit.co/download/rstudio-server/)

```bash
sudo apt-get install gdebi-core
wget https://download2.rstudio.org/server/jammy/amd64/rstudio-server-2024.12.1-563-amd64.deb
sudo gdebi rstudio-server-2024.12.1-563-amd64.deb
```

## ggplot2

## Shiny

インタラクティブな図を作るためのライブラリ。割とTidyverseをそのままでつくれる。

```
└── app  
   ├── app.R  
   ├── global.R  
   ├── server.R  
   └── ui.R
```

ディレクトリ構成はこんな感じでやるといい。一つのグラフを作るのに一つのディレクトリをつくる。サーバーとUIを分けるとわかりやすくなる。

- app.R ：Shinyを実行する。Shiny serverであればいらない。スクリプト一つでShinyを起動するために作成する。
- server.R ：サーバー側の処理でグラフの関数などを作成する
- ui.R ：動かすグラフの変数や色などのUIを設定する
- global.R ： server.Rとui.Rの両方でつかわれるライブラリ、関数等をここに書く

### 例

server.R
```R
shinyServer(function(input,output) {
  dt <-reactive({
    tibble(
      x =seq(0,1,0.1),
      y = x + input$beta*runif(length(x))      
    )
  })
  output$xyPlot <- renderPlot({
    dt() %>% ggplot() +
      geom_point(aes(x=x,y=y),size=3,color=input$color)	+
      ylim(c(0,1)) +
      annotate("text",x=0.1,y=0.9, size=10,
               label=sprintf("r=%f",cor.test(dt()$x,dt()$y)$estimate)) +
      annotate("text",x=0.1,y=0.8, size=10,
               label=sprintf("P=%f",cor.test(dt()$x,dt()$y)$p.value))
  })
  output$formula <- renderUI({
    withMathJax("$$y=\\beta x + (1 - \\beta) x'$$")
  })               
})
```

ui.R

```R
shinyUI(fluidPage(
  titlePanel("XY plot"),
  withMathJax(),
  tags$head(
    tags$style(
      HTML(
        ".MathJax {          
            font-size: 2em !important;       
          }"
      )
    )
  ),    
  sidebarLayout(
    sidebarPanel(
      sliderInput("beta",
                  "Beta:",
                  min = 0,
                  max = 1,
                  value = 0.5),
      selectInput("color",
                  "select color",
                  c("red","blue","green","black"))
    ),
    mainPanel(
      uiOutput("formula"),
      plotOutput("xyPlot")
    )
  )
))
```

global.R

```R
library(shiny)
library(shinydashboard)
library(tibble)
library(ggplot2)
```

app.R
```R
library(shiny)
runApp("../app",launch.browser=T)
```

### 埋め込み

他のサイトに埋め込む場合、
```
<iframe src="http://127.0.0.1:7858"></iframe>
```
でそのままの状態で埋め込める。

### UI

[gallery.shinyapps.io/095-plot-interaction-advanced/](https://gallery.shinyapps.io/095-plot-interaction-advanced/)
ここでほとんどのUIの例が見れる。

#### テーマ

ui.R内に以下を書く。[Bootswatch: Free themes for Bootstrap](https://bootswatch.com)を使っているのでこれのなかから良さそうなテーマを選ぶと楽。詳細なフォントや背景色を個別に設定することもできる。詳しくは[ Create a Bootstrap theme — bs\_theme • bslib](https://rstudio.github.io/bslib/reference/bs_theme.html)

ui.R
```R
theme = bslib::bs_theme(bootswatch = "darkly")
```

ui.Rを更新するとテーマが変わるがグラフ内はggplot2等で作られているのでテーマが適用されない。そのため以下をserver.Rに追加するとui.Rと同じテーマが適用される。

server.R
```
thematic::thematic_shiny()
```

ただしこれを使うと色がいい感じに配色されるがそれだけなので文字の大きさなどを変更する場合には↓のようにggplotのthemeで色々やる。その際には↑のthematicを消さないとエラーとなるので色などの配色は自分で書く必要がある。

```
ggplot() +
 ... +
 theme()
```



## Shiny server

[Shiny Server v1.5.22 Configuration Reference](https://docs.posit.co/shiny-server/)

### インストール

Ubuntu24.04

```bash
sudo apt install shiny-server 
```

トップページは↓のurlになる。ポート番号はデフォルトの場合。

```
http://localhost:3838/
```

### 基本コマンド

サーバー開始

```bash
sudo systemctl start shiny-server
```

サーバー停止

```bash
sudo systemctl stop shiny-server
```

サーバー再起動

```bash
sudo systemctl restart shiny-server
```

サーバー状態

```bash
sudo systemctl satus shiny-server
```

### 設定

基本的に`/etc/shiniy-server/shiny-server.conf`をいじる。

Rだとライブラリがインストールされている環境がユーザーごとに異なるため、shinyをどのユーザーによって実行するのか設定するといい。

```
location / {
  run_as saku;
}
```

これによって`saku`のユーザー環境でshinyが実行される。

Shiny serverによって実行されるディレクトリは↓で設定する。

```
site_dir /home/saku/Shiny:
```

## 参考

1. [R: The R Project for Statistical Computing](https://www.r-project.org)
2. [Shiny Server v1.5.22 Configuration Reference](https://docs.posit.co/shiny-server/)
3. [Rで解析：Shinyの導入と覚書](https://www.karada-good.net/analyticsr/r-638/)
4. [Shiny](https://shiny.posit.co)
5. [Welcome \| Mastering Shiny](https://mastering-shiny.org/index.html)
6. [R for Data Science (2e)](https://r4ds.hadley.nz)
7. [Bootswatch: Free themes for Bootstrap](https://bootswatch.com)
8. [【ggplot2】themeの使い方まとめ2021：作ったグラフの見た目をきれいにコントロールするために R - Qiita](https://qiita.com/ocean_f/items/03a31a8a7ce222bb3838#%E5%AF%BE%E5%BF%9C%E3%81%99%E3%82%8B%E5%BC%95%E6%95%B0%E5%90%8D%E3%81%AF%E3%81%A9%E3%81%86%E3%82%84%E3%81%A3%E3%81%A6%E6%8E%A2%E3%81%99%E3%81%8B)
9. 
