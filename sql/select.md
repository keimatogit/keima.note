# テーブルからデータを取得（SELECT）

[MySQL 5.6 リファレンスマニュアル/SELECT 構文](https://dev.mysql.com/doc/refman/5.6/ja/select.html)

<!-- @import "[TOC]" {cmd="toc" depthFrom=2 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

- [基本](#基本)
- [任意の名前で取得（AS）](#任意の名前で取得as)
- [データ数を限定して取得（LIMIT）](#データ数を限定して取得limit)
- [重複を除いて取得（DISTINCT）](#重複を除いて取得distinct)
- [レコード数を取得（COUNT）](#レコード数を取得count)
- [演算結果の取得](#演算結果の取得)
- [条件に合うデータの取得（WHERE）](#条件に合うデータの取得where)
- [グループごとの演算結果の取得（GROUP BY）](#グループごとの演算結果の取得group-by)
- [レコード（行）のソート（ORDER BY）](#レコード行のソートorder-by)
- [DATE型のカラムから年や日付を抽出](#date型のカラムから年や日付を抽出)
- [組み合わせた例](#組み合わせた例)
- [SELECT結果をファイルに保存](#select結果をファイルに保存)

<!-- /code_chunk_output -->


## 基本
```sql
-- 全カラムの全データを取得
SELECT * FROM table_name;

-- 指定カラムの値を取得
SELECT column_name1, column_name2 FROM table_name;
```
最後に `\G`オプションをつけると、レコードごとの垂直表示になる。 `\G`はセミコロンの代わりなので、セミコロンはつけない。
```sql
SELECT * FROM table_name \G
```

## 任意の名前で取得（AS）
```sql
SELECT column_name1 AS new_name1, column_name2 AS new_name2 FROM table_name;
```

## データ数を限定して取得（LIMIT）

```sql
-- 先頭10行を取得
SELECT * FROM table_name LIMIT 10;
```

## 重複を除いて取得（DISTINCT）
```sql
SELECT DISTINCT column_name FROM table_name;
SELECT DISTINCT column_name1, column_name2 FROM table_name;
`````

## レコード数を取得（COUNT）
```sql
SELECT COUNT(*) FROM table_name;
SELECT COUNT(column_name) FROM table_name;
SELECT COUNT(DISTINCT column_name) FROM table_name; -- 重複を除いたレコード数
``````

## 演算結果の取得
```sql
SELECT column_name1 + column_name2 FROM table_name;
SELECT column_name * 10 FROM table_name;
-- 平均値
SELECT AVG(column_name) FROM table_name;
SELECT AVG(column_name1 + column_name2) FROM table_name;
```

## 条件に合うデータの取得（WHERE）
```sql
SELECT * FROM table_name WHERE column_name == "character";
SELECT * FROM table_name WHERE column_name == num;
SELECT * FROM table_name WHERE column_name1 <= num1 OR column_name2 > num2;
SELECT * FROM table_name WHERE column_name BETWEEN start_value AND end_value; -- 境界値を含む
SELECT * FROM table_name WHERE column_name IS NULL;
SELECT * FROM table_name WHERE column_name IS NOT NULL;
```

## グループごとの演算結果の取得（GROUP BY）
```sql
SELECT COUNT(*) FROM table_name GROUP BY column_name1, column_name2;
SELECT AVG(column_name1) FROM table_name GROUP BY column_name2, column_name3;
```

## レコード（行）のソート（ORDER BY）
`DESC`で降順。
```sql
SELECT * FROM table_name ORDER BY column_name;      
SELECT * FROM table_name ORDER BY column_name1, column_name2;
SELECT * FROM table_name ORDER BY column_name DESC;
SELECT * FROM table_name ORDER BY column_name1 DESC, column_name2;
```

## DATE型のカラムから年や日付を抽出
```sql
SELECT YEAR(date_column) FROM table_name; -- 年を取得
SELECT DATE_FORMAT(date_column, '%D') FROM table_name; -- 日付を取得
select DATE_FORMAT(date_column,'%Y-%m') FROM table_name; -- 指定フォーマットで取得
```

## 組み合わせた例
```sql
SELECT column_name1, column_name2, COUNT(*) AS N, AVG(column_name3 + column_name4) AS mean
FROM table_name
WHERE (column_name2 BETWEEN '2016-01-01' AND '2018-12-01') AND (column_name5 < 40)
GROUP BY column_name1, column_name2
ORDER BY mean DESC;
```

## SELECT結果をファイルに保存

[13.2.9.1 SELECT ... INTO 構文](https://dev.mysql.com/doc/refman/5.6/ja/select-into.html)
リダイレクトの方が楽かも。

```sql
SELECT a,b,a+b INTO OUTFILE '/tmp/result.txt'
  [FIELDS TERMINATED BY ','] [OPTIONALLY ENCLOSED BY '"']
  [LINES TERMINATED BY '\n']
  FROM table_name;
```
