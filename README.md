# My IDE Workspace — スターターテンプレート

ライフログとLLMを連携させ、使うほど自分に最適化されていくドキュメント管理環境のテンプレートです。

## セットアップ

```bash
git clone https://github.com/KayatoX/life-context.git
cd life-context
```

**必須:**

1. `user-context/profile.md` と `mindset.md` に自分のプロフィール・価値観を書く
   - `profile.md`・`mindset.md` 以外にも、AIに知っておいてほしい情報はファイルを追加して自由に置いてOKです（例: 読書メモ・登山記録・重要な語彙など）

**任意（外部API連携が必要な場合）:**

- `.env.example` → `.env` にリネームしてAPIキーを入力
  - X（Twitter）連携: Grok API キーを設定
  - YouTube動画の要約: Gemini API キーを設定
- Notion MCP: Claude Codeで `claude mcp add` コマンドを実行してOAuth認証

あとはClaude Codeを起動するだけです。

---

## README.md と CLAUDE.md の使い分け

このリポジトリには両方が存在します。役割が違います。

| | README.md | CLAUDE.md |
|---|---|---|
| 読む対象 | **人間** | **AI（Claude Code）** |
| タイミング | リポジトリを開いたとき | Claude Codeを起動するたびに自動読込 |
| 内容 | セットアップ手順・概要説明 | AIへの指示・原則・ワークスペースの設計方針 |
| 行数 | 制限なし | **100行以内を目標**（超えるとAIの精度が落ちる） |

READMEはオンボーディング資料。CLAUDE.mdはAIへの指示書。

READMEに詳しい説明を書くほど、CLAUDE.mdをシンプルに保てます。「人間に向けた説明はREADMEへ、AIへの指示はCLAUDE.mdへ」という分担が、両方をちょうどよい長さに保つコツです。

---

## ディレクトリ構成

```
[workspace-name]/
├── README.md                    # 人間向け説明（本ファイル）
├── CLAUDE.md                    # AIへの指示書（コア）
├── .claude/
│   ├── rules/                   # 詳細ルール（遅延読み込み）
│   ├── skills/                  # スキル定義（定型ワークフロー）
│   └── agents/                  # サブエージェント定義
├── assistant/                   # エージェント自律管理領域
│   ├── user-insights.md         #   学習したユーザー傾向
│   └── log/                     #   操作ログ
├── user-context/                # 自分で追加するコンテキスト
│   ├── profile.md               #   プロフィール
│   └── mindset.md               #   価値観・思考
├── scrapbook/                   # 調べごと・インプット記録
│   ├── daily/YYYY-MM-DD/        #   テーマなし（日別）
│   └── theme/[theme-name]/      #   テーマ別に蓄積
├── project/                     # 進行中プロジェクト
└── memo.md                      # メモ
```

各ディレクトリの詳細は、それぞれの `CLAUDE.md` を参照してください。
