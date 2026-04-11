---
description: "Use when writing Python code. Covers type hints, patterns, and conventions."
applyTo: ["**/*.py"]
---
# Python Guidelines

[Google Python Style Guide](https://google.github.io/styleguide/pyguide.html) に準拠する。

## Docstring
- Google スタイルの docstring を使う（日本語で記述）
- すべての公開関数・クラス・モジュールに docstring を付ける
  ```python
  def fetch_user(user_id: int) -> User:
      """ユーザーIDからユーザー情報を取得する。

      Args:
          user_id: 取得対象のユーザーID。

      Returns:
          該当するユーザーオブジェクト。

      Raises:
          NotFoundError: ユーザーが存在しない場合。
      """
  ```

## Type Hints
- すべての関数にtype hintsを付ける
- `typing` モジュールを活用する（`Optional`, `Union`, `TypeAlias`）
- Python 3.10+ では `X | Y` 構文を使う

## Patterns
- f-string をフォーマットに使う（`.format()` より）
- リスト内包表記を適切に使う（複雑になるなら for ループに）
- コンテキストマネージャ (`with`) でリソースを管理する
- dataclass / Pydantic をデータ構造に使う

## Error Handling
- 具体的な例外をキャッチする（`except Exception` を避ける）
- カスタム例外でドメインエラーを表現する

## Project Structure
- `pyproject.toml` で依存関係を管理する
- 仮想環境 (`venv` / `uv`) を使う
