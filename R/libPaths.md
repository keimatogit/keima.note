# パッケージの場所


## パッケージの場所一覧

Rが認識しているパッケージの場所一覧を表示します。

```
.libPaths()
```

## インストール時

デフォルトでは`.libPaths()`で初めに出力される場所に保存されます。他の場所に保存する場合は`lib = "" `で指定します。
```
install.packages("tidyverse") # .libPaths()で初めに表示される場所に保存される
install.packages("tidyverse", lib = "./library") # 場所を指定して保存
```

## 読み込み時

デフォルトでは`.libPaths()`で表示される場所を探して読み込みます（.libPath()の出力順に探すので、同じパッケージが複数のフォルダにある場合は先に表示されるフォルダのものが読み込まれます）。他の場所にあるパッケージを読み込む場合は`lib.loc = "" `で指定します。

```
library(tidyverse)
library(tidyverse, lib.loc = "./library")
```

## .libPathの変更

パッケージのインストールや読み込み場所を変更したい場合、`libPath()`に指定したい場所のパスを渡すと、.libPath()の中身が指定パスとシステムのパスのみに変更されます。

```
.libPath("./library")
```
複数指定したい場合はパスをベクトルで渡します。追加したい場合は.libPath()を含めたベクトルを渡します。

```
.libPath(c(.libPaths(), "./library"))
```
