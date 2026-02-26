# 04. Issue作成・ブランチ作成

## Step 2: Issue の作成

### スキル

```
/create-issue
```

### TA の Issue 例

```markdown
## 概要
炎の柱 VFX エフェクトを作成する

## 背景・目的
ボスステージの演出として、召喚時に足元から炎の柱が上昇するエフェクトが必要。

## 実現方法
- VFX Graph で GPU パーティクルベースの炎を実装
- Custom HLSL ノードで乱流シェーダーを作成
- シーンに配置可能な Prefab として出力

## 完了条件
- [ ] VFX Graph アセット (.vfx) が作成されている
- [ ] エフェクトが Editor 上で正常に再生される
- [ ] Prefab として `Assets/VFX/Effects/Boss/` に配置されている
- [ ] モバイルで 60fps を維持できる（GPU パーティクル 500 以下）
```

### Issue の粒度

1エフェクト = 1 Issue が目安。
複数のアセットをまとめて1つの Issue にすると、PR が大きくなりすぎてレビューが困難になる。

---

## Step 3: ブランチ作成

Claude が自動でブランチを作成する。確認だけすれば OK。

### TA 向けブランチ命名規則（参考）

```
feature/<issue番号>-<アセット名>

例:
feature/12-boss-fire-pillar-vfx
feature/15-character-dissolve-shader
art/23-skybox-material-update
```
