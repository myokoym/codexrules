# rules リポジトリの汎用 rules 再編と言語別テンプレート整備

## 要約
- 今回の本丸は、`default.rules` を言語非依存の共通コアに整理し、既存のプロジェクト固有・一時回避コマンドを除去すること。
- あわせて、このディレクトリを再利用可能な rules 集約場所として成立させるため、`node.rules` と `ruby.rules` を追加する。
- 運用ルールは `AGENTS.md` に、初回セットアップや主要環境別の導入手順は `README.md` に分離し、文書のノイズを下げる。
- `AGENTS.md` には日常運用に必要な判断基準だけを書き、`README.md` には推奨ツールの `macOS(Homebrew)` / `Debian/Ubuntu(apt)` 向け導入手順をまとめる。
- Zenn 記事の思想は取り込み、探索・集計は可能な限り CLI の確定出力を優先する方針を `AGENTS.md` に反映するが、記事内の個別ツール群は今回は基礎ツール中心に絞る。

## 完了条件
- `default.rules` に既存の個別プロジェクト依存コマンドや長い `zsh -lc ...` 回避コマンドが残っていない。
- `default.rules` が探索・閲覧・比較・危険操作の少数ブロックで整理され、主要ルールに `match` / `not_match` が付いている。
- `node.rules` と `ruby.rules` が追加され、各言語の頻出コマンドを安全寄りにまとめている。
- `AGENTS.md` に、rules の責務分担、推奨ツールの存在確認、未導入時フォールバック、導入提案条件、CLI 優先原則が具体的に書かれている。
- `README.md` に、推奨ツールごとの用途と `macOS(Homebrew)` / `Debian/Ubuntu(apt)` 向け導入手順がまとまっている。
- `codex execpolicy check` で、`default.rules` と言語別 rules の代表ケースを確認できている。

## 主要マイルストーン
- 既存 `default.rules` の不要許可を棚卸しし、汎用コアへ残すものと削除するものを確定する。
- `default.rules` を共通コアとして再編する。
- `node.rules` と `ruby.rules` を追加する。
- `AGENTS.md` を追加し、日常運用ルールを固定する。
- `README.md` を追加または更新し、主要環境向け導入手順をまとめる。
- `codex execpolicy check` でルールの境界を確認する。

## 詳細タスク
1. `default.rules` から既存のプロジェクト固有コマンド、一時回避コマンド、言語依存コマンドを削除する。
2. `default.rules` を探索・閲覧・比較・危険操作の目的別ブロックに整理し、各ルールへ `match` / `not_match` を付与する。
3. `node.rules` を追加し、`npm install`、`npm run`、`npx playwright` の許可ルールを定義する。
4. `ruby.rules` を追加し、`bundle install`、`bundle update`、`bundle exec ruby`、`bundle exec bundler-audit` の許可ルールを定義する。
5. `AGENTS.md` を追加し、責務分担、推奨ツールの存在確認とフォールバック、CLI 優先原則、検証手順を記述する。
6. `README.md` を追加し、推奨ツールの用途と `macOS(Homebrew)` / `Debian/Ubuntu(apt)` 向け導入手順を記述する。
7. `codex execpolicy check` で代表的な許可ケースと要確認ケースを検証する。
