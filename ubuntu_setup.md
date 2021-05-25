---
title: "Ubuntu setup memo"
author: "matsumoto"
date: 2021/02/04
output: html
html:
  toc: true
---

# WindowsにUbuntuをインストールして環境構築

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

- [WSL2とUbuntuのインストール](#wsl2とubuntuのインストール)
- [Windows terminalを使う](#windows-terminalを使う)
- [aptコマンドでのソフト管理](#aptコマンドでのソフト管理)
- [マウントについて](#マウントについて)
  - [サーバーのマウント](#サーバーのマウント)
  - [Googleドライブのマウント](#googleドライブのマウント)
- [python環境](#python環境)
  - [pipのインストール](#pipのインストール)
  - [jupyter notebook](#jupyter-notebook)
    - [インストール](#インストール)
    - [デザイン調整](#デザイン調整)
    - [おすすめ拡張機能](#おすすめ拡張機能)
  - [ライブラリ](#ライブラリ)
- [R環境](#r環境)
  - [R](#r)
  - [Rstudio Server](#rstudio-server)

<!-- /code_chunk_output -->

メモ）`apt`と`apt-get`があるけど、基本的にaptを使用するのが良いらしい。

## WSL2とUbuntuのインストール
参考：[Windows 10 用 Windows Subsystem for Linux のインストール ガイド](https://docs.microsoft.com/ja-jp/windows/wsl/wsl2-kernel)

1. プラグラムと機能 -> Windowsの機能の有効化または無効化で「Linux用Windowsサブシステム」「仮想マシン プラットフォーム」を有効にしてPCを再起動

2. Microsoft storeからUbuntu(LTSの最新)をインストール。インストール場所のデフォルトは`C:\Users\your_user_name\AppData\Local\Packages`。

3. [Windows Subsystem for Linux インストール ガイド](https://docs.microsoft.com/ja-jp/windows/wsl/wsl2-kernel)内のリンクからWSL2をダウンロードしてインストール

Windows PowershellでWSLのバージョン確認や設定ができる
```
wsl --list --verbose             # 現在のバージョン確認
wsl --set-default-version 2      # WSL2をデフォルトに設定
wsl --set-version Ubuntu-20.04 2 # 現在のubuntuのバージョンをWSL2に変更
```

## Windows terminalを使う

Windows terminalでubuntuを使うとタブ分割ができて便利。見た目のカスタマイズもできる。

参考：[Windowsで至高のターミナル生活を求めて(Windows Terminal編)](https://www.asobou.co.jp/blog/web/windows-terminal)

1. Microsoft storeからWindows terminalをインストール
2. Windows terminalの設定をsettings.jsonに書き込む（Windows Terminalの画面上で Ctrl + , と入力するとファイルが開きます）。

settings.jsonの書き方
- defaultProfileに開きたいプロファイルのguidを指定すると、デフォルトのプロファイルを変更できる。ファイルの真ん中あたりに各プロファイルのguidが書いてあるので、Ubuntuのguideを設定しておく。（ `"$schema":〜` の下あたりに `"defaultProfile": "{************}",` を追加）
- デフォルトの見た目の設定は `"defaults"` 内に追加する。 `"fontSize": 14, "colorScheme": "Tango Dark"` など。
- wslでubuntu起動時の場所をubuntuのホームディレクトリを指定するには、ubuntu欄に`startingDirectory`を追加。`"startingDirectory" : "//wsl$/Ubuntu-20.04/home/user_name"`など。



## aptコマンドでのソフト管理

参考：[aptコマンドチートシート](https://qiita.com/SUZUKI_Masaya/items/1fd9489e631c78e5b007)

ubuntuをインストールしたら、起動して初めにパッケージ一覧の更新と入っているパッケージのアップデートをしておく
```
sudo apt update # パッケージ一覧の更新
sudo apt upgrade # パッケージのアップデート
```
インストール
```
sudo apt update # インストール前にパッケージ一覧を更新
sudo apt search package_name # パッケージを検索(部分一致)
sudo apt install package_name1 package_name2 package_name3 # インストール（複数可）
```
アップデート
```
sudo apt upgrade
```

アンインストール
```
sudo apt remove package_name
sudo apt --purge remove package_name # 依存関係があるパッケージを含めて完全に削除
```


## マウントについて

ローカルドライブは `/mnt/`  に自動的にマウントされる。

### サーバーのマウント


```
# マウントポイントを作成しておく
sudo mkdir /mnt/mount_folder

# マウント（-o ro：読み込み専用でマウント）
sudo mount [-o ro] -t drvfs '\\192.168.1.xx\xxx\xxx' /mnt/mount_folder

# マウント解除（必要なら）
sudo umount /mnt/mount_folder
```


### Googleドライブのマウント

google-drive-ocamlfuseを使います。

参考：[google-drive-ocamlfuseでGoogleドライブをマウント](https://qiita.com/cabbage_lettuce/items/c4544b3e5cd28caf04bc)
```
# インストール
sudo add-apt-repository ppa:alessandro-strada/ppa
sudo apt update
sudo apt install google-drive-ocamlfuse

# 認証
google-drive-ocamlfuse

# マウントポイントを作ってマウント
mkdir ~/GoogleDrive
google-drive-ocamlfuse ~/GoogleDrive

# マウント解除（必要なら）
fusermount -u ~/GoogleDrive
```
GUIブラウザがないときの認証
[Headless Usage & Authorization](https://github.com/astrada/google-drive-ocamlfuse/wiki/Headless-Usage-&-Authorization)
[sshごしにgoogle-drive-ocamlfuseのOAuth認証を行う方法](http://moguno.hatenablog.jp/entry/2016/03/24/010502)
Windows terminalからはできなかったので、Ubuntu本体から起動して実行しましょう。
```
echo $'#!/bin/sh\necho $* > /dev/stderr' > xdg-open
chmod 755 xdg-open
PATH=`pwd`:$PATH google-drive-ocamlfuse
```


## python環境

### pipのインストール
```
sudo apt install python3-pip
```
`pip3 install`でインストールしようとすると/home/user_name/.local/binにパスを通すよう言われるので、.bashrcに以下を追加しておく。
```
export PATH=$PATH:/home/user_name/.local/bin
```


### jupyter notebook

#### インストール
参考：[WSL2(ubuntu: 20.04)で Jupyter notebook インストールメモ](https://zenn.dev/akiyuu/articles/e6a8135858a26f2e5681)
```
sudo apt update
sudo apt install jupyter-notebook  
jupyter --version # 確認
```

`jupyter notebook --no-browser` で表示されるコピペ用URLをWindowsのウェブブラウザに貼り付ければ使用できる。



#### デザイン調整

```
# jupyterthemesをインストール
pip3 install jupyterthemes  
pip3 install --upgrade jupyterthemes

# 好きなテーマやフォントサイズを指定（-N, -Tはノート名とツールバーの表示を指定）
jt -t oceans16 -ofs 11 -T -N
```
フォントファミリーはchromの設定->デザイン->フォントをカスタマイズ->固定幅フォント欄で変えられる。

#### おすすめ拡張機能

ToC2：サイドバーにTOCを表示できる
```
pip3 install jupyter_contrib_nbextensions
jupyter contrib nbextension install --user
pip3 install jupyter_nbextensions_configurator
jupyter nbextensions_configurator enable --user
```


### ライブラリ

必要な物をpip3でインストールする。
- pandas
- numpy
- sqlalchemy
- mysql-connector-python
など。

```
pip3 install pandas numpy sqlalchemy mysql-connector-python
```

ちょっともたついたmariadbパッケージのインストール
（参考：[Problem with pip install mariadb - mariadb_config not found](https://stackoverflow.com/questions/63027020/problem-with-pip-install-mariadb-mariadb-config-not-found)）
```
sudo apt-get update -y # これと  
sudo apt-get install -y libmariadb-dev # これをを実行してから  
pip3 install mariadb
```



## R環境

### R

```
sudo apt update
sudo apt install r-base-core

# パッケージのインストールに以下の３つが必要なので入れておく。
sudo apt install libcurl4-openssl-dev
sudo apt install libssl-dev
sudo apt install libxml2-dev
```
ちなみにRのおすすめパッケージは、tidyverse（dplyrなどのパッケージ群）と、エクセルファイルを扱うならreadxl。

### Rstudio Server

参考：[Download RStudio Server for Debian & Ubuntu](https://rstudio.com/products/rstudio/download-server/debian-ubuntu/)

```
# 必要なソフトをインストール
sudo apt update
sudo apt install r-base
sudo apt install gdebi-core

# RStudio Serverをダウンロード（バージョン名は新しいものを入れること）
wget https://download2.rstudio.org/server/bionic/amd64/rstudio-server-1.4.1103-amd64.deb

# インストール
sudo gdebi rstudio-server-1.4.1103-amd64.deb

# 起動
sudo rstudio-server start
```
windowsのブラウザで `http://localhost:8787` にアクセスすると使用できる。ここで聞かれるユーザー名とパスワードはubuntuのもの。
