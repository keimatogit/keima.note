# [RMarkdown] chunk options


## 主なオプション

[Code Chunks](https://rmarkdown.rstudio.com/lesson-3.html)

- `echo = TRUE`: コード自体を表示するか
- `include = TRUE`: コード自体とコードによる出力を表示するか
- `eval = TRUE`: 実際にコードとして評価（実行）するか

- `warning = TRUE`: Warningを表示するか
- `error = TRUE`: Errorを表示するか
- `message = TRUE`: message関数の結果を表示するか（パッケージ読み込み時など）

- `fig.width = 7`: 図の幅
- `fig.height = 7`: 図の高さ
- `fig.cap = ""`: 図のキャプション



## グローバル設定

初めに`knitr::opts_chunk$set()`で指定する
`````r
```{r setup, include=FALSE}
knitr::opts_chunk$set(
  prompt  = TRUE,
  message = FALSE
)
```
`````

例）コード部分を表示せず結果だけ表示するとき
`````r
```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```
`````

## 各コードチャンクの設定

`{r }`内に書く。
`````r
```{r chunk_name, chank_option1, chunk_option2, ...}

```
`````

例）パッケージ読み込みなどの準備のとき
`````r
```{r package, include=FALSE}
library(tidyverse)
```
`````
