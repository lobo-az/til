# 宣言的UI

flutterを触っていて、UIに関する資料がないかネット上を検索したところ、
宣言的UIというタイトルのプレゼン資料を見つけた。

[宣言的UI](https://speakerdeck.com/sonatard/xuan-yan-de-ui)

ここで取り上げられているUIシステムとして、Swift UIが取り上げられている。
かつ、ReactやVue.js、flutterのUI Systemに関しても載っている。ｆ

英語では、Declarative UIと表記するらしい。

状態は別の個所で管理し、状態を保持せず、UIを描画する結果のみを宣言的に書いておくので、
宣言的UIということのようだ。

Stateをローカル・グローバルで分けて管理し、Stateの状態によってUIを制限するものが
宣言的UIである、という理解をした。

flutterのDeclarative UIの説明ページを確認する。

[Introduction to declarative UI(2020.9.20)](https://flutter.dev/docs/get-started/flutter-for/declarative)

Introduction to declarative UIより引用(2020.9.20)参照

```
In the declarative style, view configurations (such as Flutter’s Widgets) are immutable and are only lightweight “blueprints”.
To change the UI, a widget triggers a rebuild on itself (most commonly by calling setState() on StatefulWidgets in Flutter) and constructs a new Widget subtree.
```

宣言的UIの資料の通り、結果(blueprints)を宣言的に書いておいて、
状態はStateから取得し、そのときにUIの書き変わりが行われる。
