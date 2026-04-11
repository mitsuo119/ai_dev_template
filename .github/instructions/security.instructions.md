---
description: "Use when working with security-sensitive code, authentication, API endpoints, or handling user input. Covers OWASP Top 10 prevention."
---
# Security Guidelines

## Input Validation
- すべてのユーザー入力をバリデーションする
- ホワイトリスト方式を優先する（ブラックリストより）
- パラメータ化クエリを使う（SQL文字列結合を避ける）

## Authentication & Authorization
- パスワードは bcrypt/argon2 でハッシュする
- JWT の有効期限を適切に設定する
- 最小権限の原則を適用する
- セッション管理はフレームワークの仕組みを使う

## Secrets Management
- シークレットをソースコードにコミットしない
- 環境変数または secrets manager を使う
- `.env` は `.gitignore` に含める
- ログにシークレットを出力しない

## Common Vulnerabilities (OWASP Top 10)
- **Injection**: パラメータ化クエリ、ORM を使う
- **XSS**: 出力をエスケープする、CSP ヘッダーを設定する
- **CSRF**: トークンベースの保護を実装する
- **Broken Access Control**: すべてのエンドポイントで権限チェック
- **Security Misconfiguration**: デフォルト設定を変更する、不要なサービスを無効化する
