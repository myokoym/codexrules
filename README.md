# rules

Codex / CLI 系エージェント向けの再利用可能な rules 集約リポジトリです。

- `default.rules`: 言語非依存の共通コア
- `node.rules`: Node.js 系の頻出コマンド
- `ruby.rules`: Ruby / Bundler 系の頻出コマンド

詳細な運用方針は `AGENTS.md` を参照してください。ここでは推奨ツールの導入手順を管理します。

## 推奨ツール

### rg
- 用途: 高速なリポジトリ検索
- 存在確認: `command -v rg`
- macOS(Homebrew): `brew install ripgrep`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y ripgrep`

### fd
- 用途: 高速なファイル探索
- 存在確認: `command -v fd`
- macOS(Homebrew): `brew install fd`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y fd-find`
- 補足: Debian/Ubuntu では実コマンド名が `fdfind` の場合があります。

### jq
- 用途: JSON の整形、抽出、フィルタ
- 存在確認: `command -v jq`
- macOS(Homebrew): `brew install jq`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y jq`

### bat
- 用途: 見やすいファイル閲覧
- 存在確認: `command -v bat`
- macOS(Homebrew): `brew install bat`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y bat`
- 補足: Debian/Ubuntu では実コマンド名が `batcat` の場合があります。

### delta
- 用途: 差分表示の改善
- 存在確認: `command -v delta`
- macOS(Homebrew): `brew install git-delta`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y git-delta`

## 運用メモ
- 推奨ツールが無くても、まず標準コマンドで継続可能かを確認してください。
- 導入提案が必要な場合は、`AGENTS.md` の方針に従い、この README の手順を参照してください。
- 今回は基礎ツールを優先し、より高度な専用ツールは将来の拡張候補として扱います。
