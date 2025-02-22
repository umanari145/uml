# uml


## localでの環境構築
```
docker-compose up -d

http://localhost:8080
にて一般サービスと同じような画面が見れる
```
## ローカルで使う方法

*vscode限定

https://qiita.com/couzie/items/9dedb834c5aff09ea7b2

1 Javaのインストール

2 graphvizのインストール
```
brew install graphviz

# graphviz --versionなどで表示されないので注意
```

3 プラグイン　plantumlのインストール

.puファイルにシーケンス図などを書いてoption(alt) + D で右側にUML図ができる


- googleAuth.pu Oauth認証のロジック
- jwt.pu JWTの認証ロジック
- nomaltoken.pu 通常のtoken認証のロジック
- ssh.pu sshの仕組み
- stateMachine.pu ステートマシーン(https://plantuml.com/ja/state-diagram)

## mermaidによるuml
マークダウンによるuml図の作成が可能

vscodeやcursorのプラグインで表示が容易<br>
- Markdown Preview Mermaid Support


- mermaid
    - jwt.md
    - session_cookie.md
    - token.md
    - auth.md
    - oauth.md