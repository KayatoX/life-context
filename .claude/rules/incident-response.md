# インシデント対応手順

## push前セキュリティチェックリスト

```bash
# .env が git 管理されていないか確認（何も出なければOK）
git ls-files | grep "^\.env$"

# push対象のコミット差分を確認
git diff @{u}..HEAD --name-only 2>/dev/null || git diff HEAD~1 --name-only
```

チェック項目:
- [ ] `.env` が git 追跡対象になっていない
- [ ] APIキー文字列が含まれていない
- [ ] `user-context/` に機密情報が含まれていない
- [ ] `assistant/user-insights.md` に意図しない個人情報が含まれていない

---

## APIキーを誤ってコミットした場合

### Step 1: 即座にキーを無効化（最優先）

該当サービスのダッシュボードでAPIキーを失効・ローテーションする。
push済みの場合、第三者がすでに取得している可能性があるため、履歴削除より先に無効化を行う。

### Step 2: git履歴からキーを削除

**BFG Repo Cleaner（推奨）:**

```bash
# インストール
brew install bfg

# 対象ファイルを履歴から完全削除
bfg --delete-files .env

# 特定文字列を置換する場合
echo 'YOUR_SECRET_KEY=***REMOVED***' > secrets.txt
bfg --replace-text secrets.txt

# 履歴をクリーンアップ
git reflog expire --expire=now --all
git gc --prune=now --aggressive

# force push（チームへの影響を確認してから）
git push --force
```

**git filter-branch（代替手段）:**

```bash
git filter-branch --force --index-filter \
  'git rm --cached --ignore-unmatch .env' \
  --prune-empty --tag-name-filter cat -- --all
```

### Step 3: 影響確認

- GitHub push済みの場合、GitHub Supportにsecret scanningを依頼

---

## user-context/ に機密情報を書いてしまった場合

**コミット前:**
```bash
git restore user-context/該当ファイル.md
```

**コミット済み・push前:**
```bash
git reset HEAD~1
git restore user-context/該当ファイル.md
```

**push済み:** 上記BFG手順で履歴から削除する。
