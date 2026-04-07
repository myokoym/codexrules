# rules

Codex CLI の execution policy rules を置くリポジトリです。

このリポジトリの `*.rules` は、一般的なエージェント向けの行動指示ファイルではありません。`prefix_rule(...)` で「どのコマンドを `allow` / `prompt` するか」を定義する、Codex 用の許可リストです。

- `default.rules`: 言語非依存の共通コア
- `node.rules`: Node.js 系の頻出コマンド
- `ruby.rules`: Ruby / Bundler 系の頻出コマンド

`AGENTS.md` は、この許可リストをどう設計・運用するかの補助文書です。ここでは Codex 用 allowlist の役割と、推奨ツールの導入手順を管理します。

## 一括導入

macOS(Homebrew):

```bash
brew install ripgrep fd jq bat git-delta
```

Debian/Ubuntu(apt):

```bash
sudo apt-get update && sudo apt-get install -y ripgrep fd-find jq bat git-delta
```

どちらのワンライナーも `rg`、`fd`、`jq`、`bat`、`delta` を一括導入します。個別に入れたい場合は下の手順を使ってください。

## 推奨ツール

### rg
- 用途: 高速なリポジトリ検索
- 代替する標準コマンド: `git grep`、`grep`
- 存在確認: `command -v rg`
- macOS(Homebrew): `brew install ripgrep`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y ripgrep`

### fd
- 用途: 高速なファイル探索
- 代替する標準コマンド: `find`
- 存在確認: `command -v fd`
- macOS(Homebrew): `brew install fd`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y fd-find`
- 補足: Debian/Ubuntu では実コマンド名が `fdfind` の場合があります。

### jq
- 用途: JSON の整形、抽出、フィルタ
- 代替する標準コマンド: 明確な単一代替はなく、生 JSON 確認や最小限の別手段で代用
- 存在確認: `command -v jq`
- macOS(Homebrew): `brew install jq`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y jq`

### bat
- 用途: 見やすいファイル閲覧
- 代替する標準コマンド: `cat`、`sed -n`、`head`、`tail`
- 存在確認: `command -v bat`
- macOS(Homebrew): `brew install bat`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y bat`
- 補足: Debian/Ubuntu では実コマンド名が `batcat` の場合があります。

### delta
- 用途: 差分表示の改善
- 代替する標準コマンド: `git diff`
- 存在確認: `command -v delta`
- macOS(Homebrew): `brew install git-delta`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y git-delta`

## 運用メモ
- 推奨ツールが無くても、まず標準コマンドで継続可能かを確認してください。
- 導入提案が必要な場合は、`AGENTS.md` の方針に従い、この README の手順を参照してください。
- 今回は基礎ツールを優先し、より高度な専用ツールは将来の拡張候補として扱います。
