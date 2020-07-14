# Rでのデバッグ方法

とあるライブラリの関数が期待した動作を行わない。修正したい、とは思うもののRはわからない。
作者にできる限り情報を伝えたいと考えて、どうすればよいのだろうと調べ、debug関数を利用して、
関数呼び出し時にステップ実行が可能であることを知った。

```
debug(function)
```

と、Rの対話環境(RStudioなど)で行えばよい。
ステップ実行時のキー操作は、browser関数のものを参考にすればよい。

https://adv-r.hadley.nz/debugging.html#browser

# 参考

- https://github.com/joshuaulrich/quantmod/issues/310
- https://adv-r.hadley.nz/debugging.html#debug
