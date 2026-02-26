# 07. コミット・レビュー（アセット編）

## Step 5: Commit-Push-PR

### スキル

```
/commit-push-pr
```

### アセットのコミット時の注意

Unity のアセットファイルには `.meta` ファイルが必ず伴う。
**アセットと .meta は必ずセットでコミットする**。

```
Assets/VFX/Effects/Boss/FirePillar.vfx      ← コミット必須
Assets/VFX/Effects/Boss/FirePillar.vfx.meta ← 必ずセットで
```

### .gitattributes の設定

バイナリアセット（テクスチャ・FBX など）は Git LFS で管理するのが理想。
これも Claude に設定してもらえる：

```
「Unity プロジェクト用の .gitattributes を作って。
 テクスチャ（.png, .tga, .exr）、FBX、音声ファイルを
 Git LFS で管理するように設定して」
```

---

## Step 6: レビュー（GitHub Copilot）

### TA にとってのレビューの意味

プログラマーのコードレビューとは異なり、TA のレビューでは以下が主な確認事項：

- アセットの命名規則が守られているか
- フォルダ構成がプロジェクトルールに沿っているか
- 不要なアセット・重複ファイルがないか
- マテリアルのプロパティ設定の妥当性

### `.github/copilot-instructions.md` に書くべき内容（TA 向け）

```markdown
# アセットレビュー指示

## 命名規則
- VFX アセット: `VFX_<カテゴリ>_<名前>` 例: VFX_Boss_FirePillar
- シェーダー: `SH_<カテゴリ>_<名前>` 例: SH_Character_Dissolve
- マテリアル: `M_<シェーダー名>_<バリエーション>` 例: M_Dissolve_Blue

## フォルダ構成ルール
- VFX Graph: Assets/VFX/Effects/<カテゴリ>/
- Shader Graph: Assets/Shaders/<カテゴリ>/
- マテリアル: Assets/Materials/<カテゴリ>/

## コミット時の確認
- .vfx, .shadergraph には必ず .meta ファイルが伴っているか
- テクスチャは Git LFS で管理されているか
```

---

## Step 7: レビュー対応

### 流れ

1. **`/pr-review-to-plan`** でレビュー内容を基に対応プランを立てる
2. プランを確認（脳死で OK するな）
3. 対応（アセットの修正・リネームなど）
4. **`/reply-review`** でコメントに返信する

### レビューで指摘されやすい TA 案件

- 命名規則違反 → リネームして対応
- .meta ファイルの欠落 → 追加してコミット
- 不要なアセット（未使用テクスチャなど）→ 削除するか保留の理由を返信
