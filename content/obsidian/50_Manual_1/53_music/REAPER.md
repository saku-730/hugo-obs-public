---
title: REAPER
tags:
  - 2025/01
created: 2025-01-10
updated: 2025-08-31
---
###### **目次**
```toc
style:nestedList
minLevel:2
maxLevel:5
```
# REAPER

## 使い方

### 大基本

- 音声、映像、MIDIデータなどはすべて`アイテム`という扱いになる。

### Midi 

トラックを挿入後、Insert > New Midi Item または Ctrl + 左クリックで追加する。

### 書き出し

File - Render

## 設定

Options > preferences (ctrl + p)

### 初期設定(基本固定)

- インターフェース : Audio - Device よりAudio system を ASIOにする。 ASIO Driver で出力したい機器を選択する。
  ![](/obsidian/REAPER_2.png)
- VST : Plugins - VST より pathsを追加する。Edit path > Add path より`C¥ProgramFiles¥VSTPlugIns`を追加する。(なければ作成する。) このフォルダにVSTを入れていくことになる。またexeファイルで自動でインストールするような音源はこのフォルダを多くの場合、インストール先のフォルダとして選んでくれる。[2]
- 各アイテムを繰り返さない : デフォルトだと各アイテム(Midi等)を伸ばそうとするとループしていってしまう。ドラムとかなら便利だが基本的にその挙動はしてほしくないのでループをしないように変更する。Project > Item Loop Defaults から 各アイテムのループについて変更可能。
  ![](/obsidian/REAPER_1.png)

## 音源

### インストール

#### dll/vst3ファイルが配布されている場合

参考[3]

dll/vst3ファイルを`C¥ProgramFiles¥VSTPlugIns`にコピーする。

プラグインが読み込まれていない場合、preferences の Plug-ins - VST から Re-scan すると読み込まれる。

### 各音源 

#### Magical 8bit Plug 2

[Magical 8bit Plug \| YMCK Official Website](https://ymck.net/app/magical-8bit-plug/)

ピコピコ音、チップチューンの音源。日本製の中では最大手だろう。

メロディーは Pulse/Square の Duty 50%。

#### Synth1

[Software Synthesizer Synth1](https://daichilab.sakura.ne.jp/softsynth/)

シンセサイザー。

## プラグイン

Options > Show Reaper resource ~ 
でフォルダが表示されるのでそこから`UserPlugins`を開く。そこにdllファイル等を入れるとプラグインの導入が完了する。

### SWS

[SWS / S&M Extension](https://www.standingwaterstudios.com)

#### install

公式からexeファイルが配布されているので実行。

### ReaPack

[ReaPack: Package manager for REAPER](https://reapack.com)

公式からdllファイルが配布されているのでそれを`UserPlugins`に入れる。

###

## 参考

1. [なんとなくわかるREAPER｜minoba](https://note.com/minoba_sound/n/n6c4a54995dbd)
2. [\[汎用説明記事\] REAPERでのVSTの導入方法 - YTPMV.info](https://ytpmv.info/reaper-install-vst/)
3. [VST導入方法 - NiVE（にヴぇ）派](https://fear443243.hatenablog.com/entry/2023/10/25/183734)