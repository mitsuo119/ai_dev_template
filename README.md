# AI 駆動開発テンプレート

GitHub Copilot を活用した AI 駆動開発のためのプロジェクトテンプレート。

Andrej Karpathy の 4 原則と [obra/superpowers](https://github.com/obra/superpowers) の方法論をベースに、GitHub Copilot の機能をフル活用できるよう設計されています。

## 特徴

- **AGENTS.md** — プロジェクト全体に自動適用されるガイドライン（Karpathy 4 原則）
- **カスタムエージェント** — 設計・レビュー・TDD・デバッグの専用ペルソナ
- **スキル** — 頻出ワークフローをエージェントが自動で呼び出し可能な形で定義（[Agent Skills 仕様](https://agentskills.io/specification) 準拠）
- **ファイル別インストラクション** — 言語・用途に応じたルールが自動適用

## ディレクトリ構成

```
├── AGENTS.md                          # プロジェクトガイドライン（全チャットで自動読み込み）
├── LICENSE                            # MIT ライセンス
├── .gitignore
├── .vscode/
│   └── mcp.json                       # MCP サーバー設定（GitHub 連携）
└── .github/
    ├── ISSUE_TEMPLATE/                # Issue テンプレート
    │   ├── bug_report.md              # バグ報告
    │   └── feature_request.md         # 機能追加リクエスト
    ├── pull_request_template.md       # PR テンプレート
    ├── agents/                        # カスタムエージェント
    │   ├── planner.agent.md           # 設計・ブレスト
    │   ├── code-reviewer.agent.md     # コードレビュー
    │   ├── tdd.agent.md               # テスト駆動開発
    │   ├── debugger.agent.md          # 体系的デバッグ
    │   └── git-ops.agent.md           # Git 操作・ PR 作成
    ├── skills/                        # スキル（Agent Skills 仕様準拠）
    │   ├── new-feature/SKILL.md       # 新機能開発
    │   ├── fix-bug/SKILL.md           # バグ修正
    │   ├── refactor/SKILL.md          # リファクタリング
    │   ├── commit-message/SKILL.md    # コミットメッセージ生成
    │   └── create-pr/SKILL.md         # PR 説明文生成
    └── instructions/                  # ファイル別自動適用ルール
        ├── typescript.instructions.md # TS/JS ファイル
        ├── python.instructions.md     # Python ファイル
        ├── testing.instructions.md    # テストファイル
        └── security.instructions.md   # セキュリティ関連タスク
```

## 使い方

### カスタムエージェント

チャットのエージェントセレクターから選択できます。

| エージェント     | 用途                                                  |
| ---------------- | ----------------------------------------------------- |
| `@planner`       | コードを書く **前に** 要件整理・設計を行う            |
| `@code-reviewer` | コード変更のレビュー（セキュリティ・品質チェック）    |
| `@tdd`           | RED → GREEN → REFACTOR サイクルの強制                 |
| `@debugger`      | 4 フェーズの体系的根本原因分析                        |
| `@git-ops`       | コミット・プッシュ・ブランチ・ PR 作成などの Git 操作 |

### スキル

スキルはエージェントがタスクに応じて自動的に呼び出す、特定のワークフローを定義したものです。[Agent Skills 仕様](https://agentskills.io/specification) に準拠しており、バンドルアセットやエージェントの自動起動などの機能を提供します。

| スキル           | 内容                                                     |
| ---------------- | -------------------------------------------------------- |
| `new-feature`    | 新機能を設計→テスト→実装の順で開発                       |
| `fix-bug`        | バグを再現テスト→修正→検証の順で修正                     |
| `refactor`       | テストを維持しながらリファクタリング                     |
| `commit-message` | ステージ済み変更から Conventional Commits メッセージ生成 |
| `create-pr`      | ブランチの変更内容から PR 説明文を生成                   |

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
3. **`.github/skills/`** にチーム固有のスキルを追加（フォルダ + `SKILL.md` 形式）
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

## セットアップ

### 1. テンプレートからリポジトリを作成

```bash
# このテンプレートをクローン
git clone https://github.com/mitsuo119/ai_dev_template.git my-project
cd my-project

# 既存の Git 履歴を削除して新しいリポジトリとして初期化
# Linux/macOS:
rm -rf .git
# Windows (PowerShell):
# Remove-Item -Recurse -Force .git
git init
git add .
git commit -m "chore: initial commit from ai-driven template"
```

または GitHub 上で「Use this template」ボタンから新しいリポジトリを作成できます。

### 2. VS Code の設定を確認

1. VS Code で GitHub Copilot Chat 拡張機能がインストールされていることを確認
2. GitHub Copilot Pro にサインイン済みであることを確認
3. プロジェクトフォルダを VS Code で開く

テンプレート内のファイルは VS Code が自動的に認識します。追加の設定は不要です。

### 3. 動作確認

Copilot Chat を開き、以下を試してください:

- チャットで「ユーザー認証機能を追加して」と入力 → エージェントが new-feature スキルを自動起動
- エージェントセレクターから `@planner` を選択 → 設計モードで会話が始まる
- `.py` ファイルを開いて編集 → Python のインストラクションが自動適用される

## 開発ワークフロー

このテンプレートは以下のワークフローを推奨しています。

### 新機能の開発

```
1. @planner で要件整理・設計
   ↓
2. new-feature スキルが自動起動し TDD サイクルで実装
   ↓
3. commit-message スキルでコミットメッセージを生成
   ↓
4. create-pr スキルで PR 説明文を生成
```

### バグ修正

```
1. @debugger で根本原因を特定
   ↓
2. fix-bug スキルで再現テスト → 修正 → 検証
   ↓
3. commit-message スキルでコミットメッセージを生成
```

### コードレビュー

```
1. @code-reviewer で変更内容をレビュー
   ↓
2. 指摘事項を修正
   ↓
3. @code-reviewer で再レビュー
```

## よくある質問

### Q: AGENTS.md とインストラクションの違いは？

**AGENTS.md** はすべてのチャットリクエストで自動的に読み込まれるプロジェクト全体のガイドラインです。**インストラクション** (`.github/instructions/`) は特定のファイルを編集するとき、または特定のタスクを検出したときにオンデマンドで読み込まれます。

### Q: カスタムエージェントはどこから呼び出せる？

Copilot Chat のエージェントセレクター（入力欄左の `@` アイコン）から選択できます。また、他のエージェントからサブエージェントとして自動的に呼び出されることもあります。

### Q: スキルを追加するには？

`.github/skills/` に `<スキル名>/SKILL.md` フォルダを作成してください。YAML フロントマターに `name`（フォルダ名と一致、小文字英数字+ハイフン）と `description` を含めます。[Agent Skills 仕様](https://agentskills.io/specification) に準拠しています。

### Q: チーム全体で共有できる？

はい。すべての設定ファイルはリポジトリにコミットされるため、チームメンバーがクローンするだけで同じ環境が利用できます。

## 参考リンク

- [Andrej Karpathy の LLM コーディングに関する考察](https://x.com/karpathy/status/2015883857489522876)
- [obra/superpowers](https://github.com/obra/superpowers) — エージェントスキルフレームワーク
- [Agent Skills 仕様](https://agentskills.io/specification) — スキルのフォーマット仕様
- [VS Code カスタムインストラクション](https://code.visualstudio.com/docs/copilot/customization/custom-instructions)
- [VS Code カスタムエージェント](https://code.visualstudio.com/docs/copilot/customization/custom-agents)
- [VS Code カスタムスキル](https://code.visualstudio.com/docs/copilot/customization/custom-skills)

## ライセンス

[MIT](LICENSE)
