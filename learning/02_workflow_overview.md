# 02. 開発ワークフロー全体像

## 9ステップ概要

| ステップ | 内容 | スキル | 担当 |
|---|---|---|---|
| 0 | 仕様書の作成 | — | 人間 + Claude |
| 1 | プラン作成・承認 | — | 人間承認 / Claude |
| 2 | Issue 作成 | `/create-issue` | Claude |
| 3 | ブランチ作成 | — | Claude |
| 4 | 実装・検証 | `/test-unity` `/lint-unity` | Claude |
| 5 | コミット → Push → PR 作成 | `/commit-push-pr` | Claude + Hook |
| 6 | レビュー（原則1回） | — | GitHub Copilot |
| 7 | レビュー対応（修正あれば Step 4 に戻る） | `/pr-review-to-plan` → `/commit` | 人間スキル実行 → Claude |
| 8 | レビューコメントへリプライ | `/reply-review` | Claude |
| 9 | マージ（修正後の再レビューは原則不要） | — | 人間（手動） |

## 人間が必ず関与するポイント

人間の判断・操作が必要なのは以下の3箇所のみ：

1. **プランの承認**（Step 1）
2. **`/pr-review-to-plan` の実行**（Step 7）
3. **マージ**（Step 9）

それ以外は Claude Code が自動実行する。

## ポイント

- **脳死で OK するな** — プランや実装は必ず自分で読んで理解する
- プランを承認する前に、内容を把握していない場合は納得いくまで修正を求める
