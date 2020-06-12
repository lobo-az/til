# graphql-rubyでTypeの宣言を行う場合、null制約が必要

例えば、以下のような定義を行うとする

```ruby
module Types
  class User < GraphQL::Schema::Object
    field :id
    field :name
  end
end
```

こうすると、例外 `missing keyword argument null: (ArgumentError)` が出る

fieldに対しては、 `null: false` など、null制約に対する指定を必ず行わなければならない。

```ruby
module Types
  class User < GraphQL::Schema::Object
    field :id, null: false
    field :name, null: false
  end
end
```

# 参考

[[1.8] Defaulting of Field#null and Argument#required #1345
](https://github.com/rmosolgo/graphql-ruby/issues/1345)
