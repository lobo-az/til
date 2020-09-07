# WSL2 を利用して flutter アプリケーションを開発する環境を構築したい

モチベーションとして、Visual Studio Code, WSL 2 の環境を構築済みのWindows 10 環境において、
flutterのアプリケーション開発を行える環境を構築したい。

# 参考になるものはないか

Stack Over flowで、構築方法をメモしている人がいたのでそれを参考にして構築した。

[How to make Flutter work on WSL2 using host's emulator?](https://stackoverflow.com/questions/62857688/how-to-make-flutter-work-on-wsl2-using-hosts-emulator)

この記事に載っている方法は、

- WSL2上でflutterアプリケーションを動かし、Windows 10上でAndroid Emulatorを立ち上げる構成となる。
- WSL2と Windows 10上のAndroid Emulatorの通信はTCPを利用する。

# 記事に載っているやり方ではまったところ

## Android SDK

記事には、Android SDKをzipファイルとして落としてくる、とあるが、Command Line Toolだけ落とせる状態であるなど
PATHがうまく通らないことがあった。ので、Android Studio (Windows 10版)をダウンロードして、Android SDKを利用できるようにした。

## sdkmanagerによるEmulator環境の設定

記事では、avd deviceで指定しているプラットフォームが"x86"なのだが、"x86_64"のものを指定した。

`$ sdkmanager --install "system-images;android-30;google_apis;x86_64" "platform-tools" "platforms;android-29" "build-tools;29.0.3"`

- [参考](https://qiita.com/Kohei-Kato/items/1023d555403631e9b388)

## Windows 10のポート制限

ポート制限によって、WSL2, Windows 10の間の通信が行えない状態になった。
WSL2上でavd managerが通信できない旨のエラーを出したらここを疑うと良いだろう。

## Visual Studio Code

WSL2の$HOME以下にflutterをインストールしたり、Android SDKをインストールすることになるが、
ファイル数が多すぎてVisual Studio Codeがファイルのアナライズに失敗してしまう。

Visual Studio Codeで編集する場合は、flutterのソースコードがあるディレクトリを指定して
フォルダを開いて編集するようにする。そうしないと定期的にWSL2とWindows 10上のVisual Studio Codeのコネクションが切れてしまう。

# この方法には欠点があった

いざ、開発を進めていて、ホットリロードが行えない問題に行き着いた。
Windows 10上で動かしているVS Codeがflutter runで動作しているVMに接続することができない。

環境構築用に参考にしていたStack Overflowの記事に書かれていた。

https://stackoverflow.com/questions/62857688/how-to-make-flutter-work-on-wsl2-using-hosts-emulator

```
You cannot use "hot reload" features with flutter app because the process of deployment/running never finishes, however the package did be installed and running in your emulator, but for any changes in source code, you need re-run the app.
```

アプリケーションを更新するたびにflutter runを起動しなおすのはつらいので、ほかに方法がないものか検索をしてみた。
flutter runをオプション付きで起動することでJSON RPCモードで立ち上げることで、
プロセスに対してメッセージを投げてhot reload対応させるという方法があるらしい。

[手動で Flutter Android アプリに hot reload 命令を送るメモ(2020 年 1 月 14 日時点)](https://qiita.com/syoyo/items/37d5f22689bb50217858)

しかし、これもまた手間がかかる。

OSネイティブで開発を進めてしまったほうが楽なのかもしれない。

# ADB カスタム Socket設定未対応

Flutterは、2020/9/7現在、ADBのカスタム Socket通信未対応とのことであった。

[Support custom ADB sockets while debugging](https://github.com/flutter/flutter/issues/61604)

`flutter attach` について、リモートマシンに対して実行可能になれば問題が解決する。
