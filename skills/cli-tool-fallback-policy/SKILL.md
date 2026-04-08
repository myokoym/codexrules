---
name: cli-tool-fallback-policy
description: ターミナルでの作業において、rg、fd、jq、bat、git diff、delta を優先し、それらがない場合の代替手段を明示する。リポジトリ検索、ファイル一覧表示、JSON 操作、ファイル閲覧、差分表示の際に使う。
---

# CLI ツール優先とフォールバック

- **リポジトリ検索**は `rg` を優先する。
  - 例: `rg <pattern>`, `rg -n <pattern> .`, `rg --files`
  - `rg` が無ければ `git grep <pattern>`、必要なら `grep -R <pattern> .`
- **ファイル探索**は `fd` を優先する。
  - 例: `fd <name>`, `fd -t f <pattern>`
  - `fd` が無ければ `fdfind`、それも無ければ `find . -name '<name>'`
- **JSON の整形・抽出**は `jq` を優先する。
  - 例: `jq . file.json`, `jq -r '<filter>' file.json`
  - `jq` が無ければ生 JSON を確認し、必要最小限の別手段で代替する。
- **ファイル閲覧**は `bat` を優先する。
  - 例: `bat <file>`
  - `bat` が無ければ `batcat`、それも無ければ `sed -n '1,80p' <file>`、`cat <file>`、`head`、`tail`
- **差分**はまず `git diff` を使う。
  - 例: `git diff -- <path>`, `git diff --stat`
  - `delta` が使えるなら見やすい表示に使ってよい。
  - `delta` が無ければ通常の `git diff` のまま。
