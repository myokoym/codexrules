---
name: cli-tool-fallback-policy
description: Directs terminal work to prefer rg, fd, jq, bat, and git diff (optionally delta) with explicit fallbacks when those tools are missing. Use when searching the repo, listing files, handling JSON, viewing files, or showing diffs from the shell.
---

# CLI ツール優先とフォールバック

## 適用

このスキルが有効なときは、シェル経由の作業で次の優先順とフォールバックに従う。他ファイル（例: `AGENTS.md`）への追記やユーザー環境の編集を手順に含めない。

## 方針

- **リポジトリ検索**は `rg` を優先する。
  - 例: `rg <pattern>`, `rg -n <pattern> .`, `rg --files`
  - `rg` が無ければ `git grep <pattern>`、必要なら `grep -R <pattern> .`
- **ファイル探索**は `fd` を優先する。
  - 例: `fd <name>`, `fd -t f <pattern>`
  - `fd` が無ければ `fdfind`（Debian/Ubuntu のパッケージ名差）、それも無ければ `find . -name '<name>'`
- **JSON の整形・抽出**は `jq` を優先する。
  - 例: `jq . file.json`, `jq -r '<filter>' file.json`
  - `jq` が無ければ生 JSON を確認し、必要最小限の別手段で代替する。
- **ファイル閲覧**は `bat` を優先する。
  - 例: `bat <file>`
  - `bat` が無ければ `batcat`、それも無ければ `sed -n '1,120p' <file>`、`cat <file>`、`head`、`tail`
- **差分**はまず `git diff` を使う。
  - 例: `git diff -- <path>`, `git diff --stat`
  - `delta` が使えるなら見やすい表示に使ってよい。
  - `delta` が無ければ通常の `git diff` のまま。
