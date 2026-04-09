# rules

Codex CLI の execution policy rules を置くリポジトリです。

このリポジトリの `*.rules` は、一般的なエージェント向けの行動指示ファイルではありません。`prefix_rule(...)` で「どのコマンドを `allow` / `prompt` するか」を定義する、Codex 用の許可リストです。

- `default.rules`: 言語非依存の共通コア
- `node.rules`: Node.js 系の頻出コマンド
- `ruby.rules`: Ruby / Bundler 系の頻出コマンド

このリポジトリの `AGENTS.md` は編集用です。通常利用時に Codex へ読ませたいフォールバック方針は、下のテンプレートを `~/.codex/AGENTS.md` に追記して使います。

## `~/.codex/AGENTS.md` への追記例

普段使いで Codex にフォールバック方針を読ませたい場合は、`~/.codex/AGENTS.md` に次のような節を追記します。

```md
## CLI フォールバック方針
- リポジトリ検索は `rg` を優先する。
  - 例: `rg <pattern>`, `rg -n <pattern> .`, `rg --files`
  - `rg` が無ければ `git grep <pattern>`、必要なら `grep -R <pattern> .`
- ファイル探索は `fd` を優先する。
  - 例: `fd <name>`, `fd -t f <pattern>`
  - `fd` が無ければ `find . -name '<name>'`
- JSON の整形や抽出は `jq` を優先する。
  - 例: `jq . file.json`, `jq -r '<filter>' file.json`
  - `jq` が無ければ生 JSON を確認し、必要最小限の別手段で代替する。
- ファイル閲覧は `bat` を優先する。
  - 例: `bat <file>`
  - `bat` が無ければ `sed -n '1,120p' <file>`、`cat <file>`、`head`、`tail`
- 差分確認はまず `git diff` を使う。
  - 例: `git diff -- <path>`, `git diff --stat`
  - `delta` が使える環境では、`git diff` の見やすい表示に使ってよい。
  - `delta` が無ければ通常の `git diff` をそのまま使う。
```

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
- 補助する標準コマンド: `git diff`
- 存在確認: `command -v delta`
- macOS(Homebrew): `brew install git-delta`
- Debian/Ubuntu(apt): `sudo apt-get update && sudo apt-get install -y git-delta`

## 運用メモ
- 推奨ツールが無くても、まず標準コマンドで継続可能かを確認してください。
- 導入提案が必要な場合は、この README の手順と上の `~/.codex/AGENTS.md` テンプレートを使って運用してください。
- 今回は基礎ツールを優先し、より高度な専用ツールは将来の拡張候補として扱います。

## License

このリポジトリの内容は、別途明記がない限り [`CC0 1.0 Universal`](LICENSE) ([`CC0-1.0`](https://creativecommons.org/publicdomain/zero/1.0/)) で提供します。

将来、第三者由来のテキストやコード断片を追加する場合は、その部分の元ライセンス表示を保持し、必要ならこのリポジトリの `CC0` 対象外であることを明記してください。
