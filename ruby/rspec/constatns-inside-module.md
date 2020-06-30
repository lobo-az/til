# Moduleに定義されている定数や、ロードを行う処理のテストをどう行うか

以下のようなmoduleがあるとする。

```ruby
module TestModule
  GET_HTTP = TestHttpModule::HTTP::Get.fetch("http://example.com")
end
```

そしてこのmoduleは、Railsアプリケーション内のlibディレクトリで定義されている。

```
  lib/test_module.rb
```

Rails Applicationが立ち上がると、`test_module.rb`がautoloadの機能によって読みだされるようになっている。
すると、`TestModule`に定義されている定数に代入を行う

`TestHttpModule::HTTP::Get.fetch("http://example.com")`

という処理が評価される。
この処理の評価時に、例外が発生するとRails Applicationのプロセスは立ち上がらなくなる。

このような問題が発生し、対応したあと、さてrspecをどのように書くとよいのだろうか、とちょっと悩んでいた。

- test_module.rb が読み込まれるときに問題がでる
- rspecでのテスト時に、`include TestModule`を書くだけで済むのだろうか?

やり方を探し、見つけた方法は以下の書き方だった。

```ruby
describe 'test' do
  context 'load test_module' do
    it 'raise error' do
      expect { load Rails.root.join('lib/test_module.rb') }.to raise_error
    end
  end
end
```

# 参考

- [module function Kernel.#load](https://docs.ruby-lang.org/ja/latest/method/Kernel/m/load.html)
