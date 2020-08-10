# default_scopeを外したい場合に利用するunscopedの影響

以下のようなassociationがあるとする

```ruby
class User < ActiveRecord::Base
  has_many :messages
end
```

```ruby
class Message < ActiveRecord::Base
  belong_to :user
  
  default_scope { where(created_at: (Time.now - 10.days)..Time.now) }
end
```

ここで、例えば以下のようにunscopedを利用する

```ruby
> user = User.find(1)
> user.messages.unscoped
```

この、`user.messages`の問い合わせは、UserのIDで絞り込んだMessageとなりそうであるが、
unscopedはすべてのリレーション・mergeの関係を取り去ってしまうため、Messageすべてが返ってきてしまう。

`user.messages`が吐き出すSQL文は以下となる

```ruby
  Message Load (0.2ms)  SELECT "messages".* 
    FROM "messages" WHERE "messages"."created_at" 
    BETWEEN ? AND ? AND "messages"."user_id" = ? LIMIT ? 
    [["created_at", "2020-07-31 15:31:26.624900"], ["created_at", "2020-08-10 15:31:26.624936"], ["user_id", 1], ["LIMIT", 11]]
=> #<ActiveRecord::Associations::CollectionProxy [#<Message id: 1, user_id: 1, created_at: "2020-08-10 15:29:32", updated_at: "2020-08-10 15:29:32">, #<Message id: 2, user_id: 1, created_at: "2020-08-10 15:29:38", updated_at: "2020-08-10 15:29:38">]>
```

`user.messages.unscoped`が吐き出すSQL文は以下となる

```ruby
  Message Load (0.1ms)  SELECT "messages".* FROM "messages" LIMIT ?  [["LIMIT", 11]]
=> #<ActiveRecord::Relation [#<Message id: 1, user_id: 1, created_at: "2020-08-10 15:29:32", updated_at: "2020-08-10 15:29:32">, #<Message id: 2, user_id: 1, created_at: "2020-08-10 15:29:38", updated_at: "2020-08-10 15:29:38">, #<Message id: 3, user_id: 2, created_at: "2020-08-10 15:29:47", updated_at: "2020-08-10 15:29:47">]>
```

うっかりが発生しがちなので注意

# 参考

[Ruby on Rails 6.0.3.2 ActiveRecord::Scoping::Default::ClassMethods](https://api.rubyonrails.org/classes/ActiveRecord/Scoping/Default/ClassMethods.html#method-i-unscoped)
