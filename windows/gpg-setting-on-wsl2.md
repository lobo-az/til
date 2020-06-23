# WSL2上のUbuntu 20.04で、gpgsign有効化を行った後にgit commitに失敗する

gpg keyを生成して、git configで設定を施していざ `git commit -S` を実行した後、エラーとなってしまった。

```
error: gpg failed to sign the data
fatal: failed to write commit object
```

なぜだろう？と調べていくと以下のissue commentに行き着いた。

https://github.com/microsoft/WSL/issues/4029#issuecomment-491512157

GPG_TTYという環境変数に、ttyコマンドが返す端末デバイスを設定しなければならないということを知った。
これを設定した後、

`echo "test" | gpg --clearsign`

このコマンドを実行したら、testという結果に対して、署名がついた形で正常に出力された。

```
-----BEGIN PGP SIGNED MESSAGE-----
Hash: SHA512

test
-----BEGIN PGP SIGNATURE-----

iQIzBAEBCgAdFiEEXhSoGphFRmW6fbmaP1O1EfubRXQFAl7yEHwACgkQP1O1Efub
RXTs0hAAinOILMdrrmtp73nKy+nEr/yFkx726lJtaVOUkEqJbDX/3BNx7UCRcE65
82m6o/bYGDdYH+RPOhPUY7ERTHny1wCr6L11XV4b1BaKq7AW6B2+TiOam4NE84xk
NCISU85R8T5asrJRGqXSHikpX2mTuF/+UDTfXqf9aWyDrs5meikM1iVrq+s0PCQR
ufwQt0bHrNNVT1uCn28FVNnZiafKfcgKDZBV0j+r9KdrM+vT/4w0mcyC1FnxPiee
IIzhCrECBSQYWw+MF1ykH2OCbhi9ddbLT+FWST23J+7gZBcm5qCKYPxyPrLAaBCP
eV2VQfbhKMTckBL9H6hGXyjUo4w2CT72cYXfycoX9V73DBbqGGtT6R9/FXLP0/Ll
QYquA33679SoQgQrjYROrQOC1TwhC3BU8kDHaqwVt5SMBTF7YLm0ulOduCpKE/1X
KGULyg3ghFenp5CDK3jseYYiii1KMavjrQEsgySzVcYriiyDRdbtvM310XtgdKuS
vjfik65qqF/mkjQSOFe9OL8rlqjfaFo9juPcjXb8qMJ5ofxpLZCvABZB6h8FammV
N+nI91+P/+mBMsHl8VRbPaAow8G2QIGS3/2xVKrv2Uc63ThpjhmEEq94SMY7hA6i
/DPUdwhE/jOaM3mii4trKt+kPk3kU4z8UEPwqCkZ1rGQ1HvDhCM=
=sjEE
-----END PGP SIGNATURE-----
```
