# PostgreSQLでは、ADD COLUMN AFTER col_name は利用できない。

MySQLでは、ADD COLUMNに対して、AFTER col_name を指定することで
この列以降に、新しい列を追加するというオプションを指定することが可能となっている。

[13.1.9 ALTER TABLE Statement](https://dev.mysql.com/doc/refman/8.0/en/alter-table.html)

より構文を引用

```sql
ALTER TABLE tbl_name
    [alter_option [, alter_option] ...]
    [partition_options]

alter_option: {
    table_options
  | ADD [COLUMN] col_name column_definition
        [FIRST | AFTER col_name]
```

対して、PostgreSQLでは、AFTERオプションは存在しない。

https://www.postgresql.jp/document/12/html/sql-altertable.html

```
ADD COLUMN [ IF NOT EXISTS ]
```

そのため、列を好みの箇所に指定をしたい場合は、
新規テーブルを作って、列の順序を整えて、元テーブルを削除する方法をとらなければならない。
