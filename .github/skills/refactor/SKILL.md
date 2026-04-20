---
name: refactor
description: "Refactor code while maintaining all existing behavior and test coverage. Use when the user wants to restructure or improve code quality without changing functionality."
---

# Refactor

次のコードをリファクタリングしてください: {ユーザーからの指示}

## ワークフロー

1. 既存のテストがすべてパスすることを確認する
2. リファクタリングの計画を立てる
3. 小さなステップで変更する（1ステップ = 1論理的変更）
4. 各ステップ後にテストを実行する
5. すべてのテストがパスすることを最終確認する

## 注意事項

- 振る舞いを変更しない
- テストカバレッジを下げない
- 一度に複数の変更をしない
