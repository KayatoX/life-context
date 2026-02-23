# Skills

Claude Codeに「定型の作業手順」を覚えさせるファイル群。

## 追加方法

`.claude/skills/[skill-name]/SKILL.md` を作成する。
YAMLフロントマターに `name` と `description` を書くと、関連するタスクのときだけ自動で読み込まれる。

```yaml
---
name: skill-name
description: このスキルが何をするかの説明（1行）
---

# スキル名

## 手順
...
```

## 同梱スキル

| スキル | 説明 |
|---|---|
| `commit-workflow` | git コミット〜プッシュの全手順を漏れなく実行。意思決定ログ・インサイト更新・ライティングルール更新を含む |

`/commit` または「コミットして」で呼び出す。

## 参考

- [Claude Code 公式ドキュメント](https://code.claude.com/docs)
- [awesome-claude-skills](https://github.com/travisvn/awesome-claude-skills)
