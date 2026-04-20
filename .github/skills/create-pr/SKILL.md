---
name: create-pr
description: "Generate a pull request description from branch changes. Use when the user wants to create a PR or needs a PR description."
---

# Pull Request Description Generator

現在のブランチの変更内容を確認し、PR説明文を生成してください。

## 手順

1. ベースブランチを特定する（デフォルト: `main`。プロジェクトにより `master` や `develop` の場合あり）
2. `git log <base>..HEAD --oneline` でコミット履歴を確認
3. `git diff <base>...HEAD --stat` で変更ファイルを確認
4. 主要な変更内容を分析

## PR テンプレート

```markdown
## 概要

{この PR が何を解決するかの1-2文の説明}

## 変更内容

- {主要な変更点をリストアップ}

## テスト

- [ ] 既存テストがパスする
- [ ] 新しいテストを追加した
- [ ] 手動テストで動作確認した

## スクリーンショット（UI変更がある場合）

{該当する場合のみ}

## 関連Issue

{関連するIssue番号}
```
