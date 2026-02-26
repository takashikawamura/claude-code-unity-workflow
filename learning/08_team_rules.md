# 08. Rules / Skills / Hooks（TA 向け）

## Rules

### 概要

`.claude/rules/` に書いたルールは Claude が自動的に参照する。
毎回指示しなくても Claude がプロジェクトのルールに従ってくれる。

### TA が書くべき Rules の例

#### `unity-asset-rules.md`

```markdown
# Unity アセット管理ルール

## 命名規則
- VFX Graph: VFX_<カテゴリ>_<名前>
- Shader Graph: SH_<カテゴリ>_<名前>
- マテリアル: M_<シェーダー名>_<バリエーション>
- テクスチャ: T_<対象>_<種別>  例: T_Grass_Albedo, T_Grass_Normal

## フォルダ構成
Assets/
  VFX/
    Effects/    ← VFX Graph アセット
    Textures/   ← VFX 用テクスチャ
  Shaders/
    Characters/
    Environment/
    Effects/
  Materials/
    Characters/
    Environment/

## パフォーマンス規則
- モバイル向け VFX: GPU パーティクル 500 以下
- シェーダーの Instruction 数: 200 以下推奨
```

#### `shader-coding-rules.md`

```markdown
# シェーダーコーディング規則

## HLSL Custom Function
- 関数名は PascalCase
- 入力変数名は in_ プレフィックス、出力は out_ プレフィックス
- URP 互換コードで書く（Built-in RP 専用コードは使わない）

## パフォーマンス
- pow() より smoothstep() を優先
- ループは静的展開を優先（[unroll] アトリビュート）
- tex2D より SAMPLE_TEXTURE2D マクロを使う（URP 対応）
```

---

## Skills

### TA 向けのスキル例

| スキル | 用途 |
|---|---|
| `/create-issue` | Issue 作成 |
| `/lint-unity` | Unity 特有ルールのチェック（命名規則・フォルダ構成） |
| `/commit-push-pr` | Commit → Push → PR 自動化 |
| `/pr-review-to-plan` | レビュー内容をプランに変換 |
| `/reply-review` | レビューコメントへの返信 |

### TA 独自スキルの追加案

```markdown
# /check-assets スキル
Assets/ フォルダを走査して、命名規則違反・
孤立した .meta ファイル・未使用アセットを一覧で報告する
```

---

## Hooks

### TA に有効なガードレール例

```
- main / develop への直接 push を禁止
- .meta ファイルなしのアセットコミットを検出して警告
- 巨大ファイル（50MB 以上）のコミットを警告
```

---

## .claude/ ディレクトリの構成例（TA 向け）

```
.claude/
  CLAUDE.md                      プロジェクト全体のルール
  rules/
    unity-asset-rules.md         アセット命名・フォルダ規則
    shader-coding-rules.md       シェーダーコーディング規則
    git-workflow.md              Git 運用ルール
  skills/
    create-issue.md
    lint-unity.md
    commit-push-pr.md
    pr-review-to-plan.md
    reply-review.md
```

`.claude/` は常にアップデートして改善する（**ウナギのたれ**）。
アセット管理・シェーダー規則などを蓄積していくほど Claude の精度が上がる。
