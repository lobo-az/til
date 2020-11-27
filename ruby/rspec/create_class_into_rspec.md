# rspec内にclassを作る

テスト対象とするクラスをrspecのdescribe block内にclassを作りたい場合は、以下のやり方を取ることができる

```ruby
describe 'test' do
  before do
    test_class = Class.new(SuperClass) do
      def calc
        @x + @y
      end
    end
    
    stub_const('TestClass', test_class)
  end
  
  context 'calculate' do
    let!(x) { 10 }
    let!(y) { 30 }
    
    subject do
      TestClass.new(x, y)
    end
  
    it 'return result' do
      expect(subject.calc).to eq(x + y)
    end
  end
end
```

## 参考

https://relishapp.com/rspec/rspec-mocks/v/3-10/docs/mutating-constants
