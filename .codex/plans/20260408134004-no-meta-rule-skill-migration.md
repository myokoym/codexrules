# `.cursor` のメタ禁止ルールを汎用 skill へ移す実装 plan

## 要約

- 今回の本丸は、`.cursor/rules/no-meta-in-production-docs.mdc` にある「正規文書本文へ経緯メタを混ぜない」原則を、新しい repo 内 skill へ移し、旧 `.cursor` ルールを削除すること。
- 既存の `cli-tool-fallback-policy` など別論点には広げず、この原則の移設だけで完結させる。
- 追加する skill は、正式な指示文書やルール本文に不要な経緯説明、反省、会話ログ、使い方メタを入れない原則を定義する。
- 正規文書の例は `AGENTS.md`、`SKILL.md`、`*.rules`、ルール文書、ポリシー文書とし、背景説明の退避先はコミットメッセージ、PR、調査メモ、ADR と明示する。

## 完了条件

- `skills/no-meta-in-canonical-docs/SKILL.md` が追加されている。
- `.cursor/rules/no-meta-in-production-docs.mdc` が削除されている。
- skill 本文が、禁止事項と必須事項を自己完結した形で記述している。
- 既存ファイルへの不要な変更が入っていない。
- 差分確認と最小限の検証結果を添えてコミットできる状態になっている。

## 主要マイルストーン

- 新規 skill の名前と責務を確定する。
- skill 本文を作成し、対象、禁止、必須を記述する。
- 旧 `.cursor` ルールを削除し、置き換えを完了する。
- 差分と体裁を確認する。
- plan を保存し、コミット単位を確定する。

## 詳細手順

1. 新しい skill 名を `no-meta-in-canonical-docs` とし、正規文書本文に不要なメタ説明を入れない原則専用の skill にする。
2. `skills/no-meta-in-canonical-docs/SKILL.md` を追加し、次の内容を含める。
   - 対象: 利用者やエージェントが参照してそのまま従う正式な本文
   - 禁止: 経緯、反省、会話ログ、移行理由、本文の使い方だけを説明するメタ段落
   - 必須: 規約、手順、事実のみを書くことと、背景の退避先
3. `.cursor/rules/no-meta-in-production-docs.mdc` を削除し、新しい skill へ置き換える。
4. 既存の `cli-tool-fallback-policy` や `*.rules` など別論点はこの作業では編集しない。
5. `git status --short`、`git diff --check`、差分確認で、意図した変更だけが入っていることを確かめる。
6. コミット時は、日本語メッセージで skill 追加と旧 `.cursor` ルール削除を簡潔に記す。
