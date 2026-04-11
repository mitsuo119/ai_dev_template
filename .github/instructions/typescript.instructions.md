---
description: "Use when writing TypeScript or JavaScript code. Covers type safety, patterns, and conventions."
applyTo: ["**/*.ts", "**/*.tsx", "**/*.js", "**/*.jsx"]
---
# TypeScript / JavaScript Guidelines

## Type Safety
- `any` の使用を避ける。不明な型には `unknown` を使う
- 型アサーション (`as`) より型ガードを優先する
- 戻り値の型を明示する（推論が曖昧な場合）

## Patterns
- `null` チェックにはオプショナルチェイニング (`?.`) を使う
- Nullish coalescing (`??`) を `||` より優先する
- `enum` より as const オブジェクトを優先する
- 非同期処理は async/await を使う（.then チェーンより）

## Error Handling
- エラーは型安全にキャッチする: `catch (error: unknown)`
- カスタムエラークラスでエラーの種類を区別する
- エラーメッセージは具体的かつアクション可能にする
