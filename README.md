# AI 駆動開発テンプレート

GitHub Copilot を活用した AI 駆動開発のためのプロジェクトテンプレート。

Andrej Karpathy の 4 原則と [obra/superpowers](https://github.com/obra/superpowers) の方法論をベースに、GitHub Copilot の機能をフル活用できるよう設計されています。

## 特徴

- **AGENTS.md** — プロジェクト全体に自動適用されるガイドライン（Karpathy 4 原則）
- **カスタムエージェント** — 設計・レビュー・TDD・デバッグの専用ペルソナ
- **プロンプトテンプレート** — 頻出ワークフローを `/` コマンドで即座に実行
- **ファイル別インストラクション** — 言語・用途に応じたルールが自動適用

## ディレクトリ構成

```
├── AGENTS.md                          # プロジェクトガイドライン（全チャットで自動読み込み）
├── .gitignore
└── .github/
    ├── agents/                        # カスタムエージェント
    │   ├── planner.agent.md           # 設計・ブレスト
    │   ├── code-reviewer.agent.md     # コードレビュー
    │   ├── tdd.agent.md               # テスト駆動開発
    │   └── debugger.agent.md          # 体系的デバッグ
    ├── prompts/                       # プロンプトテンプレート（/ で起動）
    │   ├── new-feature.prompt.md      # 新機能開発
    │   ├── fix-bug.prompt.md          # バグ修正
    │   ├── refactor.prompt.md         # リファクタリング
    │   ├── commit-message.prompt.md   # コミットメッセージ生成
    │   └── create-pr.prompt.md        # PR 説明文生成
    └── instructions/                  # ファイル別自動適用ルール
        ├── typescript.instructions.md # TS/JS ファイル
        ├── python.instructions.md     # Python ファイル
        ├── testing.instructions.md    # テストファイル
        └── security.instructions.md   # セキュリティ関連タスク
```

## 使い方

### カスタムエージェント

チャットのエージェントセレクターから選択できます。

| エージェント     | 用途                                               |
| ---------------- | -------------------------------------------------- |
| `@planner`       | コードを書く **前に** 要件整理・設計を行う         |
| `@code-reviewer` | コード変更のレビュー（セキュリティ・品質チェック） |
| `@tdd`           | RED → GREEN → REFACTOR サイクルの強制              |
| `@debugger`      | 4 フェーズの体系的根本原因分析                     |

### プロンプトテンプレート

チャットで `/` を入力するとテンプレート一覧が表示されます。

| コマンド          | 内容                                                     |
| ----------------- | -------------------------------------------------------- |
| `/new-feature`    | 新機能を設計→テスト→実装の順で開発                       |
| `/fix-bug`        | バグを再現テスト→修正→検証の順で修正                     |
| `/refactor`       | テストを維持しながらリファクタリング                     |
| `/commit-message` | ステージ済み変更から Conventional Commits メッセージ生成 |
| `/create-pr`      | ブランチの変更内容から PR 説明文を生成                   |

### 自動適用インストラクション

対象ファイルを編集するときに、対応するルールが自動的にコンテキストに読み込まれます。

| ルール     | 適用対象                                     |
| ---------- | -------------------------------------------- |
| TypeScript | `*.ts`, `*.tsx`, `*.js`, `*.jsx`             |
| Python     | `*.py`                                       |
| Testing    | `*.test.*`, `*.spec.*`, `test/`, `tests/`    |
| Security   | セキュリティ関連タスク検出時（オンデマンド） |

## 基本原則

Andrej Karpathy の指摘する LLM コーディングの課題に対する 4 つの原則:

1. **コーディング前に考える** — 仮定を明示し、不明確なら確認する
2. **シンプルさ優先** — 要求されたことだけを、最小限のコードで実装する
3. **外科的な変更** — 関係ないコードに触らない
4. **ゴール駆動の実行** — タスクを検証可能なゴールに変換し、テストで確認する

## カスタマイズ

### プロジェクト固有の設定を追加するには

1. **AGENTS.md** にビルドコマンド、アーキテクチャ情報、プロジェクト固有の規約を追記
2. **`.github/instructions/`** にフレームワーク固有のルールを追加（例: `react.instructions.md`）
3. **`.github/prompts/`** にチーム固有のワークフローを追加
4. **`.github/agents/`** にドメイン特化エージェントを追加

### 例: React プロジェクト用インストラクションの追加

```yaml
---
description: "React コンポーネントの作成時に使用。hooks、パターン、規約をカバー。"
applyTo: ["src/components/**/*.tsx", "src/pages/**/*.tsx"]
---
# React ガイドライン
- 関数コンポーネント + hooks を優先する
- React.memo は計測済みのパフォーマンス改善がある場合のみ使用する
```

## 必要条件

- [GitHub Copilot Pro](https://github.com/features/copilot) サブスクリプション
- VS Code + GitHub Copilot Chat 拡張機能

## 参考リンク

- [Andrej Karpathy の LLM コーディングに関する考察](https://x.com/karpathy/status/2015883857489522876)
- [obra/superpowers](https://github.com/obra/superpowers) — エージェントスキルフレームワーク
- [VS Code カスタムインストラクション](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [VS Code カスタムエージェント](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [VS Code プロンプトファイル](https://code.visualstudio.com/docs/copilot/customization/prompt-files)

## ライセンス

MIT
