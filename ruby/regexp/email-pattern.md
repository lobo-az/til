# emailアドレスかどうか、正規表現を利用したいがパターンを用意するのがどうすればよいのかわからない場合

[URI::MailTo](https://github.com/ruby/ruby/blob/b0b6d0a68854c637b9be63f3af178eb4eb285fc1/lib/uri/mailto.rb)以下に、メールアドレスの正規表現パターンが定義されていた。

https://github.com/ruby/ruby/blob/b0b6d0a68854c637b9be63f3af178eb4eb285fc1/lib/uri/mailto.rb#L55 よりコードを引用。


```ruby
    # practical regexp for email address
    # https://html.spec.whatwg.org/multipage/input.html#valid-e-mail-address
    EMAIL_REGEXP = /\A[a-zA-Z0-9.!\#$%&'*+\/=?^_`{|}~-]+@[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?(?:\.[a-zA-Z0-9](?:[a-zA-Z0-9-]{0,61}[a-zA-Z0-9])?)*\z/
```

WHATWGのWHTML文書へのリンクがコメントとして書かれている。

https://html.spec.whatwg.org/multipage/input.html#valid-e-mail-address より、書かれている文書を引用する。

```html
A valid email address is a string that matches the email production of the following ABNF, the character set for which is Unicode. This ABNF implements the extensions described in RFC 1123. [ABNF] [RFC5322] [RFC1034] [RFC1123]
```

RFCへのリンクがあり、インターネット上で扱うメッセージフォーマット、アドレスの定義に基づいた
正しいメールアドレスに合致する正規表現の組み合わせらしい。
