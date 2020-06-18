# WSL2上では、カスタマイズされたLinux KernelとWindows 10どちらもHyper-V上で動作する

https://twitter.com/Liliaceae/status/1269629966318096385?s=19

```
結構誤解されているぽいですが、最近のハードで Windows 10 を動かしている場合、
CPU から見た OS は Hyper-V のハイパーバイザーで、Windows 10 は Hyper-V の上にいることが多いです。
意識していないと思いますがセキュリティのため仮想化されています。msinfo32 を昇格して実行すると確認できます。
```

元ソースとして以下のプレゼンテーションで説明されている。

https://youtu.be/lwhMThePdIo?t=1789

他、解説している個人ブログも参考になる

[ついにDockerに対応したWSL2を私見で解説してみた](https://koduki.hatenablog.com/entry/2019/05/10/124945)
