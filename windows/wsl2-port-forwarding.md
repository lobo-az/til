# WSL2上のプロセスが利用しているtcpポートについて、ホスト側からlistenしたい場合

[ビルド 18945](https://docs.microsoft.com/ja-jp/windows/wsl/release-notes#build-18945)より

```
[WSL2] localhost:port を使用して、WSL2 のリスニング tcp ソケットにホストからアクセスできるようにします
```

```
[wsl2]
kernel=<path>              # An absolute Windows path to a custom Linux kernel.
memory=<size>              # How much memory to assign to the WSL2 VM.
processors=<number>        # How many processors to assign to the WSL2 VM.
swap=<size>                # How much swap space to add to the WSL2 VM. 0 for no swap file.
swapFile=<path>            # An absolute Windows path to the swap vhd.
localhostForwarding=<bool> # Boolean specifying if ports bound to wildcard or localhost in the WSL2 VM should be connectable from the host via localhost:port (default true).

# <path> entries must be absolute Windows paths with escaped backslashes, for example C:\\Users\\Ben\\kernel
# <size> entries must be size followed by unit, for example 8GB or 512MB
```

デフォルトはtrueらしい。ということは設定不要なのか。
実際に試してみる。


```
nc -l 8080
```

で、wsl2側に8080ポートで待ち受けられる状態にして、実際にホスト側のブラウザからアクセスすると

```
GET / HTTP/1.1
Host: localhost:8080
Connection: keep-alive
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/83.0.4103.106 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Accept-Language: ja,en;q=0.9,en-US;q=0.8
```

リクエストヘッダが送られてきていた。
WSL2便利だなあ。
