# 06. Commit → Push → PR

## Step 5: Commit-Push-PR

### スキル

```
/commit-push-pr
```

### 自動化の仕組み

Claude + Hook によって以下が自動化される：

1. `git commit` — 変更をコミット
2. `git push` — リモートブランチへプッシュ
3. PR 作成 — GitHub に Pull Request を作成

### セットアップ方法

公式プラグインを入れると楽：

```
/plugin から commit-commands を追加
```

### PR の内容

自動生成される PR には以下が含まれる：

- **Summary** — 変更内容の箇条書き
- **Test plan** — テスト・動作確認の手順チェックリスト
- 関連 Issue への参照（`Closes #XX`）

### Hook の役割

- `main` / `develop` への直接 push を禁止するガードレール
- CI/CD のトリガー
