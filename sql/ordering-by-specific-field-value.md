# 特定の値だけ優先的に先頭・末尾に並べた状態をORDER BYで実現するにはどうすればよいのか

以下の書き方を行えば良い

```
ORDER BY user_id = 100, user_id DESC
```

`user_id = 100` に合致する行が有る場合ソート順序に優先的に並び替えが実施される。

PostgreSQLでは動作を確認した。他のSQL実装でも同じようになるかも。

注意: SQL標準の文書を参照して書いたわけではないので実装により差があるかも。

参考: https://dba.stackexchange.com/questions/154814/how-to-return-rows-with-a-specific-value-last
