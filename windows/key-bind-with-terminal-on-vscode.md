# VSCodeのTerminalでemacsキーバインドを利用したい

Shellのhistoryを戻すためにCtrl+p, Ctrl+nを利用する。
Ctrl+fも、コマンドの行末に移動するために利用をする。

Windows + VSCodeで実行すると、Ctrl+fはファイル内での文字列検索状態になってしまう。
キーバインドの設定は行えないのか調べてみた。すると簡単に設定を書き換えることで実現できることがわかった。

[VS CodeからWSLに繋いで統合ターミナルでemacs風キーバインドを使う](https://qiita.com/tkykmw/items/3aa6c80f6d17175eb731)
[Integrated Terminal](https://code.visualstudio.com/docs/editor/integrated-terminal)

こちらより設定の内容をコピーペーストする。

-- keybindings.json

```json
[
    {
        "key": "ctrl+a",
        "command": "workbench.action.terminal.moveToLineStart",
        "when": "terminalFocus"
    },
    {
        "key": "ctrl+e",
        "command": "workbench.action.terminal.moveToLineEnd",
        "when": "terminalFocus"
    },
    {
        "key": "ctrl+f",
        "command": "-workbench.action.terminal.focusFindWidget",
        "when": "terminalFocus"
    }
]
```

- setting.json

```json
{
    "terminal.integrated.commandsToSkipShell": [
        "-workbench.action.quickOpen",
    ]
}
```
