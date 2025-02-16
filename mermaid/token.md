```mermaid
sequenceDiagram
    actor User
    participant Client
    participant APIServer
    participant Database
    
    User->>Client: 入力ログイン情報
    Client->>APIServer: POST
    APIServer->>Database: ユーザー認証確認
    Database-->>APIServer: 認証結果
    
    alt 認証成功
        APIServer->>APIServer: ランダムトークン生成
        APIServer->>Database: トークンとユーザー情報を保存
        APIServer-->>Client: トークン返却
        Client->>Client: トークンを保存
        Client-->>User: ログイン成功表示
    else 認証失敗
        APIServer-->>Client: 認証エラー (401)
        Client-->>User: エラーメッセージ表示
    end
    
    Note over Client,APIServer: 保護されたAPIへのアクセス
    Client->>APIServer: リクエスト + Authorization: Bearer {token}
    APIServer->>Database: トークン検証
    Database-->>APIServer: ユーザー情報
    APIServer-->>Client: APIレスポンス
    
    Note over Client,APIServer: ログアウト
    Client->>APIServer: POST
    APIServer->>Database: トークン無効化
    APIServer-->>Client: ログアウト成功
    Client->>Client: トークン削除
```

メリット：
1. APIとの親和性
- HTTPヘッダーでの認証が標準的
- クロスプラットフォームでの実装が容易
- モバイルアプリなどでも扱いやすい

2. セキュリティ管理
- トークンの即時無効化が可能
- トークンの有効期限管理が容易
- アクティブなセッション（トークン）の把握が容易

3. 実装の柔軟性
- トークンに紐づく情報の管理が自由

デメリット：
1. パフォーマンス
- 毎リクエストでDBアクセスが必要
- トークン検証のオーバーヘッド
- DBへの負荷が高い

2. スケーラビリティ
- トークン情報のDB同期が必要
- 分散システムでの管理が複雑
- DBのボトルネック

使い分けのポイント：
1. アプリケーションの性質
- Webアプリケーション中心 → セッション認証
- API中心のシステム → トークン認証

2. スケール要件
- 単一サーバー/小規模 → セッション認証
- 大規模/分散システム → トークン認証

3. クライアントの多様性
- ブラウザのみ → セッション認証
- 多様なクライアント → トークン認証