# deep copy

JavaScriptで、deep copyを行いたい場合どうするべきなんだろうと調べると、

`JSON.parse(JSON.stringify(object))` を使うと良い、と出てきた。

なるほど、原理を考えるとそりゃそうだ。これは手軽な方法である。

# 参考

- [Native deep cloning](https://stackoverflow.com/questions/122102/what-is-the-most-efficient-way-to-deep-clone-an-object-in-javascript/122704#122704)
