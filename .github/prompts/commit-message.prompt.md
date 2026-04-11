---
description: "Generate a conventional commit message for staged changes"
agent: "agent"
tools: [execute, read]
---

# Commit Message Generator

現在のステージされた変更（`git diff --cached`）を確認し、Conventional Commits 形式のコミットメッセージを生成してください。

## フォーマット

```
<type>(<scope>): <日本語の説明>

<body>
```

## ルール

- type: feat, fix, docs, refactor, test, chore のいずれか（英語）
- scope: 変更の影響範囲（英語、省略可）
- subject: 日本語で簡潔に記述、末尾に句点なし、50文字以内
- body: 何を変更したかではなく、なぜ変更したかを説明
- 例: `feat(認証): ログイン画面にパスワードリセットリンクを追加`
