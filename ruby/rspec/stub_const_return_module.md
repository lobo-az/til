# stub_const を利用すると、名前空間をmoduleとして利用するようになる

例えば、以下のようなclassが2つあるとする。

```ruby
class BaseClass
  TEST_CONST = 100
end

class SubClass < BaseClass
  def number
    TEST_CONST
  end
end
```

`SubClass` をテストするコードを書く。

```ruby
describe SubClass do
  context 'stub_const test' do
    let(:number) { 200 } 
  
    before do
      stub_const("BaseClass::TEST_CONST", number)
    end
    
    let(:sub_class_instance) { described_class.new }
    
    it 'get number' do
      expect(sub_class_instance.number).to eq(number)
    end
  end
end
```

このexampleを実行すると、BaseClassがModuleとなるためエラーが出てしまう。

```ruby
TypeError (superclass must be a Class (Module given))
```

回避方法がないか調べてみたところ、rspec-mocks プロダクトリポジトリのissueで問題が取り上げられていた。

https://github.com/rspec/rspec-mocks/issues/1079

このIssueにかかれている内容を調べてみる。すると、

```
It creates it as a module since modules are so often used as namespaces (e.g. MyGemModule::SomeClass)
```

と書かれており、ModuleかClassかは、rspec-mocksでのmock段階では不明なのでModuleとして、名前空間を切るようにしているようである。
他のコメントにて

`stub_const("#{MODEL}::CONST, 2)` とすることで、実行時評価を行うようにして対応しているというものがあった。
試してみたら正常に動いた。

```ruby
describe SubClass do
  context 'stub_const test' do
    let(:number) { 200 } 
  
    before do
      stub_const("#{BaseClass}::TEST_CONST", number)
    end
    
    let(:sub_class_instance) { described_class.new }
    
    it 'get number' do
      expect(sub_class_instance.number).to eq(number)
    end
  end
end
```


# 参考

- https://github.com/rspec/rspec-mocks/issues/1079
- https://github.com/rspec/rspec-mocks/issues/1079#issuecomment-215491725
- https://github.com/rspec/rspec-mocks/issues/1079#issuecomment-215620243
