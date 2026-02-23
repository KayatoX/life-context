# セキュリティガイドライン

## user-context/ に入れてはいけない情報

以下は `user-context/` に置かない（git管理対象のため公開リスクあり）:

- 銀行口座・クレジットカード情報
- パスワード・PINコード
- 医療記録・健康情報（センシティブな内容）
- 仕事上の機密情報・NDA対象情報
- 他人のプライバシーに関わる情報

AIへの指示・ルールは `user-context/` ではなく `.claude/rules/` または `CLAUDE.md` に書く。

## APIキー管理

- APIキーは必ず `.env` に置く（`.gitignore` 追加済み）
- CLAUDE.md・Skills・user-context/ にAPIキーを直接書かない
- `.env.example` には実際のキーを書かない（形式例のみ）

## MCPスコープ設定

NotionMCPを設定する際:

1. **ワークスペース全体の権限を与えない** — 対象ページ・DBのみを選択
2. **読み取り専用に制限する** — 書き込み・削除権限は最小限に
3. **定期的に権限を見直す** — 不要なページへのアクセスを削除

## プロンプトインジェクション対策

`user-context/` には「自分の情報」だけを書く。以下は書かない:

- ❌ AIへの命令・指示（例:「今後はすべての会話で〜してください」）
- ❌ 他のファイルを読み込む指示
- ❌ 外部URLを参照する指示

## pre-push hook のインストール

`.githooks/pre-push` をgit hookとして有効化:

```bash
git config core.hooksPath .githooks
chmod +x .githooks/pre-push
```

インシデント対応 → `.claude/rules/incident-response.md` を参照。
