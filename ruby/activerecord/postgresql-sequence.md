# Rails + PostgreSQLの組み合わせでPrimary Keyを指定して更新した際のsequence値

Railsのmigrationで作成されるテーブルに指定されているPrimary Keyは、defaultの値として
nextvalによるSequence値のインクリメントが指定されている。

https://github.com/rails/rails/blob/d9bfafd9b8af6d3ee099d6a3d431744b70666aac/guides/source/active_record_postgresql.md#database-views

で、このような構造になっているとき、

```ruby
Post.create(id: 1000, text: 'hello world')
```

のように、ActiveModelのcreateメソッドを利用し、レコードを追加すると
レコードのidは1000と指定されるが、本来defaultの値として入るはずであった
`nextval`関数は呼ばれず、Sequence値はインクリメントされない。

```ruby
Post.create(text: 'hello world!!')
```

とコンソールで実行を行うと、もしPost(postsテーブル)への
レコード作成が初めてであったとするなら、Sequence値は1となる。

## この動作で問題が起きることはあるのか?

アプリケーションの作り方によって、すでに存在しているレコードのバックアップとして、
外部からデータをimportする場合に、id = 1, id = 2と指定していたとする。

外部からのレコードインポート処理を終えた後に、
通常通り、アプリケーション側のレコード生成処理ではidを指定しないようにする、
するとSequence値が1,2...から始まることになる。

Primary Keyはunique制約が入ってるとすると、例外となる。

## Sequence値を更新する

手動でSequenceの値を更新することで解消することはできる。
(setvalを利用するなど)

## Sereal型の採用を考える

デフォルトで作成されるidに指定される型はint8指定であったりするので、migration時に型
Serial型を指定してしまうのもよいと考えられる。

https://www.postgresql.jp/document/12/html/datatype-numeric.html

しかし、Serial型はPostgres独自の型であるため、ほかのDBMSへの移行を行うのであれば
変換スクリプトを用意する必要がある。その時は用意するとは思うが。

