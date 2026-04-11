---
description: "Use when writing or modifying tests. Covers testing patterns, naming conventions, and anti-patterns."
applyTo: ["**/*.test.*", "**/*.spec.*", "**/test/**", "**/tests/**", "**/__tests__/**"]
---
# Testing Guidelines

## Naming
- テスト名は振る舞いを説明する: `should return empty array when no items match filter`
- Arrange-Act-Assert パターンを使う

## Principles
- 実装ではなく振る舞いをテストする
- テスト間に依存関係を作らない
- モックは最小限に（外部サービスのみ）
- エッジケースを必ず含める: 空入力、境界値、無効データ

## Anti-patterns
- テスト内のロジック（if/for）を避ける
- テスト間で状態を共有しない
- スナップショットテストに過度に依存しない
- テストの中で複数のことをアサートしすぎない
