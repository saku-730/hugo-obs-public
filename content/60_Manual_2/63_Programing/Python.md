---
title: Python
tags:
  - 2024/06
created: 2024-06-15
updated: 2026-04-12
---
クソみたいな環境でおなじみ。

## 環境構築

Linuxでは特にデフォルトでシステム用にPythonがインストールされておりそれをいじるとシステムに不具合が起こることがある(一敗)。そのため必ず仮想環境を準備する。Pythonは仮想環境以外でいじらない。

### [mamba forge](https://github.com/mamba-org/mamba)

anacondaをC++で作り直して効率化したやつ。ライブラリ自体はcondaと同じのが使えてanacondaよりも速くて安定しているので今の所これが一番いい。[miniforge](https://github.com/conda-forge/miniforge)はmamba forgeのインストーラーみたいな位置づけ。

デフォルトだとbase環境が常に起動するが個人的にはこれはpython以外を使っている間に問題が起こりかねないと思っているので
```
conda config --set auto_activate_base false
```
↑でデフォルトで起動しないようにする。

#### install 

```
wget "https://github.com/conda-forge/miniforge/releases/latest/download/Miniforge3-$(uname)-$(uname -m).sh"
bash Miniforge3-$(uname)-$(uname -m).sh
```

基本全部yesかEnterでいい。

#### 基本コマンド

環境作成
```
mamba create -n [name] python=
```
環境一覧
```
mamba info -e
```

#### 環境移植

仮想環境をyamlで出力。
```
mamba env export > ファイル名.yml
```
ファイル名をしてしなければ内容だけ見れる。

yamlファイルを元に仮想環境を構築
```
mamba env create -n 環境名 -f ファイル名.yml
```



### anaconda

定番。GUIもあって初心者がとりあえず使えって言われるけどGUIがあるだけで別に使いやすいかと言われればそうでもない。クソ重い。GUI使うと結局何しているのかわからなくなりがち。無駄な(別でインストール済みの)Rstudioとかも一緒にインストールされてしまったりわけわからなくなる原因を多くはらんでいる。その点で微妙。これを初心者におすすめするのどうなん?

### Pyenv

使ってる人はまあまあいる。とりあえずならこれでいいとも思う。

### UV

#### install

```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```



## パッケージ

pipで基本入れることになるがconda推奨はcondaで入れよう。tensolflow絡みとか。pipとcondaを共存させるとろくなことにならないので必ずどちらか片方のみにする。

いつからかpythonの仮想環境でないとpipでのインストールができなくなった。くそやんけ。対処法としては仮想環境を何かしら使うか、pipではなくaptで入れる。

## 機械学習系

### Pytorch

[PyTorch](https://pytorch.org)

#### Install

[Get Started](https://pytorch.org/get-started/locally/)で必要なバージョンとかを決めてインストール

pythonバージョンは3.9-3.12で作っておけば問題なし。

#### 

