# 08. チーム開発での Claude 動作の共通化（Rules / Skills / Hooks）

## Rules

### 概要

`CLAUDE.md` と同様に**自動読み込みされる**設定ファイル群。
リポジトリの `.claude/rules/` ディレクトリに配置する。

参考: https://code.claude.com/docs/ja/memory

### 共通化すべき内容

| カテゴリ | 内容例 |
|---|---|
| アーキテクチャ | レイヤー構成、命名規則、依存関係のルール |
| ヒエラルキールール | Unity Hierarchy の命名・構造ルール |
| アセット命名規則 | スクリプト・シーン・Prefab の命名規則 |
| コーディング規約 | スタイル、コメント規則、禁止パターン |
| Git 運用ルール | ブランチ戦略、コミットメッセージ規則 |

---

## Skills

### 概要

定型作業をスキル（コマンド）として共通化する。
参考: https://code.claude.com/docs/ja/skills

### 主なスキル

| スキル | 用途 |
|---|---|
| `/create-issue` | Issue 作成 |
| `/test-unity` | Unity TestRunner 実行 |
| `/lint-unity` | Unity 特有ルールのチェック |
| `/commit-push-pr` | Commit → Push → PR 自動化 |
| `/pr-review-to-plan` | レビュー内容をプランに変換 |
| `/reply-review` | レビューコメントへの返信 |

コマンドとしても自然言語ベースでも使える。

---

## Hooks

### 概要

Claude やメンバーがやってはいけない操作への**ガードレール**。
参考: https://code.claude.com/docs/ja/hooks

### 代表的な Hook

```
main / develop への直接 push を禁止
```

### メリット

- 人間も Claude も間違える → 自動で止める
- 致命的な操作を未然に防ぐ

---

## .claude/ ディレクトリの構成例

```
.claude/
  CLAUDE.md               プロジェクト全体のルール
  rules/
    architecture.md       アーキテクチャルール
    unity.md              Unity固有ルール
    git.md                Git運用ルール
  skills/
    create-issue.md
    test-unity.md
    commit-push-pr.md
    pr-review-to-plan.md
    reply-review.md
```

`.claude/` は常にアップデートして改善する（**ウナギのたれ**）。
実装よりもこちらのアップデートに注力すると実装が安定する。
