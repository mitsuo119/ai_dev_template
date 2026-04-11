---
description: "Generate a conventional commit message for staged changes"
agent: "agent"
tools: [execute, read]
---
# Commit Message Generator

現在のステージされた変更（`git diff --cached`）を確認し、Conventional Commits 形式のコミットメッセージを生成してください。

## フォーマット
```
<type>(<scope>): <subject>

<body>
```

## ルール
- type: feat, fix, docs, refactor, test, chore のいずれか
- scope: 変更の影響範囲（省略可）
- subject: 命令形、小文字始まり、末尾にピリオドなし、50文字以内
- body: 何を変更したかではなく、なぜ変更したかを説明
