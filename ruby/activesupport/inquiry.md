# Rails.env.production? で ENV["RAILS_ENV"] == "production" を判別できるのはなぜ？

inquiryというString classに追加したメソッドを利用するためだ。

[5.7 inquiry](https://guides.rubyonrails.org/active_support_core_extensions.html#inquiry) より

```ruby
"production".inquiry.production? # => true
"active".inquiry.inactive?       # => false
```

https://github.com/rails/rails/blob/v6.0.3.2/activesupport/lib/active_support/core_ext/string/inquiry.rb

# rspecで環境変数ごとによるテストを書きたい場合

こういう需要がたまにでてくる。その場合は以下のように書けばよい。

```ruby
describe TestClass do
  
  context 'is production' do
    before do
      allow(Rails).to receive(:env).and_return('production'.inquiry)
    end
    
    it 'result is production' do
      expect(describe_class.new.environment).to eq('production')
    end
  end
  
  context 'is development' do
    before do
      allow(Rails).to receive(:env).and_return('development'.inquiry)
    end
    
    it 'result is development' do
      expect(describe_class.new.environment).to eq('development')
    end
  end
end
```
