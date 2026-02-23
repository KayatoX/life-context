# .claude/

Claude Code の設定・ルール・スキルを管理するディレクトリ。

## ディレクトリ構成

```
.claude/
├── README.md                    # 本ファイル
├── rules/                       # 詳細ルール（CLAUDE.mdから分離）
├── skills/                      # スキル定義（定型ワークフロー）
├── agents/                      # サブエージェント定義
└── settings.local.json.example  # MCP・ツール設定の構造例
```

## rules/

CLAUDE.mdから分離した詳細ルールを置く場所。Claude Codeの遅延読み込みにより、該当パスにアクセスしたときだけ自動的に読み込まれる。

| ファイル | 内容 |
|---|---|
| `writing-style.md` | 文体・ライティング方針（自分のフィードバックで育てる） |
| `characters.md` | キャラクターモード定義（好みのキャラを追加していく） |

→ `rules/README.md` に詳しい作り方あり

## skills/

Claude Codeに定型の作業手順を覚えさせるスキル定義。`/スキル名` で呼び出す。

→ `skills/README.md` に詳しい作り方あり

## agents/

サブエージェントの定義ファイル。特定タスクのために自律的に動かすエージェントをここに定義する。

→ `agents/README.md` に詳しい説明あり

## settings.local.json

Claude CodeがMCP接続・ツール実行許可を記録するファイル。**gitignore対象**（コミットしない）。
Notion MCPなどの接続設定は `claude mcp add` コマンドで自動記録される。
`settings.local.json.example` に構造例を置いているので参考にどうぞ。
