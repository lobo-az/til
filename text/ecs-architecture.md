# ECS (Entity Component System)

ECSは、ゲームプログラミングにおいて、敵オブジェクトなどの継承によるオブジェクト生成に関する課題を解決するために整理をされたプログラミングアーキテクチャである

[Entity component system(Wikipedia)](https://en.wikipedia.org/wiki/Entity_component_system)

[古典的ゲームループからECSアーキテクチャまで](https://zenn.dev/rita0222/articles/c22a8367e31b4d5f4eeb)

オブジェクトごとに状態を保持し、update メソッドを呼び出して更新を行うようなObserverパターンを採用するとメモリ効率が悪いので、
状態を持つオブジェクトである `Component` を別途、キャラクタオブジェクトとは異なるオブジェクトとして管理を行うことで、
更新処理を一括して行えるようにしたもの、と上記の`zenn.dev` による記事で紹介されている。

欠点は存在していて、親子関係を持つ場合と、処理を行う順序をオブジェクトごとに任意に操作したい場合には
管理を行う方法を探さなければならない。その場合はOberserパターンを利用し、
update methodを呼び出すことでObjectの状態更新を行う方法も有用であろう。
