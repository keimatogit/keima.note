# conda環境

```
wget https://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh

bash
conda config --add channels conda-forge
conda config --add channels defaults
conda config --add channels r
conda config --add channels bioconda
```
```
conda update conda
conda update --all
```



Jupyter notebbok拡張機能

新しいnbconverttではdownload html with tocができず、5.6.1にしたらできた。
```
conda install jupyter
conda install jupyter_contrib_nbextensions
conda install "nbconvert=5.6.1"
```

jupyter notebookでRを使う
[jupyter notebookでRを使う](https://nxdataka.netlify.app/rjup/)
```
conda install  -c r r r-irkernel r-essentials [rstudio] -y
```
データベース接続関連
```
conda install mysql-connector-python sqlalchemy
```

そのほか
```
conda install pandas
```
