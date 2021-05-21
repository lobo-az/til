# マルチコアCPUの動作周波数を調べたいとき

https://twitter.com/m_bitsnbites/status/1138429974560616448?s=20

この方法が使える。

```
watch -n 0.1 'cat /proc/cpuinfo | grep MHz'
```
