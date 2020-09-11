# Intel SGXについて

雑談でIntel SGXについて話があがった。
知らなかった事柄であった。ネット上の文書検索で見つかる範囲の記事をまとめておく。

# 簡単にまとめると

- Intel SGXテクノロジーは、飛び地領域といわれるメモリ領域がある
- 飛び地領域はEnclaveといわれる
- Enclaveで扱われるデータは暗号化され、保護される

# 用途は何があるか

## DRM

以下の記事では、UHD BDを再生する際にIntel SGXテクノロジーを利用していることが記載されている
  
[いよいよ立ち上がるUHD BDのPC再生環境 (PC Watch)](https://pc.watch.impress.co.jp/docs/column/ubiq/1040708.html)

```
具体的にはソフトウェア側で暗号化鍵を持って解除することは認められず、
ハードウェアによるセキュアな環境で暗号化鍵を解除する必要がある。

このため、再生ソフトウェア(パイオニアのUHD BDドライブにはCyberLinkの「PowerDVD 14」がバンドル)は、
Intel SGXを利用して暗号化鍵の解除を行なう仕組みになっている。Intel SGXとは、
Intelの第6世代Coreプロセッサ(開発コードネーム：Skylake)の一部製品から導入が始まった、セキュアなソフトウェアの実行環境。
```

## プライバシー保護

プライバシー保護に利用する目的で研究を行った報告を見つけた。

[Intel SGXによるプライバシー保護 生命情報解析プラットフォーム 櫻井 碧, 岩田 大輝, 清水 佳奈](https://www.cbio.cs.waseda.ac.jp/assets/materials/IIBMP2019_poster.pdf)

## 遠隔認証

[Intel SGX - Remote Attestation概説 https://qiita.com/Cliffford](https://qiita.com/Cliffford/items/095b1df450583b4803f2)
[Intel Software Guard Extensionのチュートリアルを読む(1. SGX Foundation) https://msyksphinz.hatenablog.com/entry/2018/08/21/040000](https://msyksphinz.hatenablog.com/entry/2018/08/21/040000)

話の中で、遠隔認証が出てきたのでネット検索で出てきた記事を見てみると、Intel Software Guard Extensionのチュートリアルを読む(1. SGX Foundation)の記事に概要が書かれていた。

```
Remote Attestationでは、サードパーティのサーバを使用して認証を獲得するのだが、
そのためのくおーとを生成するためにIntel SGXソフトウェアとハードウェアを使用する。
```

Intel自身がサーバのサービスを運用しているようだ。

https://software.intel.com/content/www/us/en/develop/topics/software-guard-extensions/attestation-services.html
https://software.intel.com/content/www/us/en/develop/articles/intel-enhanced-privacy-id-epid-security-technology.html
