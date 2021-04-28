# インデックス(key)について

[MySQL のインデックスの使用の仕組み](https://dev.mysql.com/doc/refman/5.6/ja/mysql-indexes.html)

インデックスを作成したカラムは値の検索がすばやくできる。
Primary Key(主キー)に指定したカラム、Foreign Key(外部キー)制約を指定したカラムには、自動的にインデックスが作成されるので、明示的にインデックスを作成する必要はない。

## インデックス情報の取得

データベース中のインデックス情報を取得
```sql
select TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, INDEX_NAME
from INFORMATION_SCHEMA.STATISTICS
where TABLE_SCHEMA='database_name';
```

テーブル中のインデックス情報を取得
```sql
select TABLE_SCHEMA, TABLE_NAME, COLUMN_NAME, INDEX_NAME
from INFORMATION_SCHEMA.STATISTICS
where TABLE_NAME='table_name';
```

テーブルの詳しいインデックス情報を取得
[SHOW INDEX 構文](https://dev.mysql.com/doc/refman/5.6/ja/show-index.html)
```sql
SHOW INDEX FROM table_name;
```


## インデックスの追加と削除

追加
（複合インデックスの場合はカラム名をカンマ区切りで指定）
```sql
ALTER TABLE table_name ADD INDEX [index_name](column_name);
ALTER TABLE table_name ADD INDEX [index_name](column_name1, column_name2);
```

削除
```sql
ALTER TABLE table_name DROP INDEX index_name;
```
