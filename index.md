# keima.note

いわゆる忘備録です。

## python
- [データベースを使用する(MariaDB)](python/database.md)
- [seabornサンプルデータの使い方](python/sample_data.md)
- [グラフ](python/graphs.md)
- [ipywidgetsで動的グラフを作る](python/ipywidgets.md)

## R
- [データベースを使用する（MariaDB）](R/database.md)
- [mutateでも使える条件分岐（if_else, case_when, recode, (factor)）](R/mutate2.md)
- [factor型について](R/factor.md)
- [パッケージの場所（.libPaths()）](R/libPaths.md)
- [renvを使用したパッケージ管理](R/renv.md)
- [パッケージの作り方](R/make_package.md)
- [[Rmarkdown] 準備](R/rmd_prepare.md)
- [[Rmarkdown] YAMLヘッダー](R/rmd_yaml.md)
- [[Rmarkdown] chunk options](R/rmd_chunk.md)


## データベース・SQL
DBMSはMySQL派生のMariaDBを使用しています。MySQLとはあまり変わらないと思います。

準備とDB操作
- [環境設定（MariaDBのインストールと起動）](sql/mariadb_install.md)
- [DBサーバーへの接続とSQLの実行方法](sql/execute_sql.md)
- [DBユーザーの管理](sql/user.md)
- [データベースの操作](sql/database.md)

テーブルの管理と構造
- [テーブルの操作](sql/table.md)
- [インデックス（キー）](sql/sql_index.md)
- [外部キー制約、check制約](sql/constraint.md)

データの書き換え
- [レコード（行）の追加・編集・削除](sql/record.md)
- [csvファイルのインポート(LOAD DATA INFILE)](sql/csv_import.md)

データの取得
- [テーブルからデータを取得（SELECT）](sql/select.md)
- [テーブルの結合（JOIN）](sql/join.md)

その他
- [MySQLサンプルデータの使い方](sql/sample_data.md)


## その他
- [コマンドラインでのプログラム実行時に引数を扱う（python, R, shell）](commandargs.md)
- [githubの使い方](github.md)
- [Guthub Pagesの使い方](github_pages.md)
- [singularityの使い方](github.md)
- [WindowsにUbuntuをインストールして環境構築](ubuntu_setup.md)
- [ssh接続でホスト名を登録](ssh_hostname.md)
- [テキストエディタATOM](atom.md)
