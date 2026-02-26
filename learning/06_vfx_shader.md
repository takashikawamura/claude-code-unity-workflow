# 06. VFX Graph / Shader Graph での Claude 活用

---

## VFX Graph

### ファイル形式

`.vfx` ファイルは **JSON 形式**。Claude がそのまま読んで内容を理解できる。

```
「Assets/VFX/Effects/Boss/FirePillar.vfx を読んで、
 ノード構成の概要を説明して」
```

### Claude に頼めること

| 作業 | 例 |
|---|---|
| ノード構成の提案 | 「乱流のある炎を VFX Graph で作る構成を提案して」 |
| .vfx ファイルのレビュー | 「このファイルで不要なノードや最適化できる箇所はある？」 |
| パーティクル数の削減提案 | 「モバイル向けに GPU パーティクル 200 以下に抑えたい」 |
| ループ設定の確認 | 「このエフェクトがループしない理由を調べて」 |

### Custom HLSL in VFX Graph

VFX Graph の Custom HLSL Block は Claude と一緒に書ける。

```hlsl
// 例: 乱流によるオフセット
float3 TurbulenceOffset(float3 position, float time, float strength)
{
    float3 offset;
    offset.x = sin(position.z * 2.1 + time * 0.7) * strength;
    offset.y = cos(position.x * 1.8 + time * 0.9) * strength * 0.5;
    offset.z = sin(position.y * 2.3 + time * 0.6) * strength;
    return offset;
}
```

---

## Shader Graph

### ファイル形式

`.shadergraph` ファイルは **JSON 形式**。Claude がそのまま読める。

```
「Assets/Shaders/Character/Dissolve.shadergraph を読んで、
 ディゾルブの処理フローを説明して」
```

### Claude に頼めること

| 作業 | 例 |
|---|---|
| シェーダーアルゴリズムの設計 | 「UV スクロールとノイズを組み合わせた水面シェーダーの構成を提案して」 |
| Custom Function の HLSL 実装 | 「Voronoi ノイズを Custom Function で実装して」 |
| .shadergraph のレビュー | 「このシェーダーでモバイルのパフォーマンスに問題がある箇所は？」 |
| エラーの原因調査 | 「Shader Graph がコンパイルエラーになっている。ファイルを読んで原因を教えて」 |

### Custom Function ノードの HLSL

Shader Graph の Custom Function ノードの HLSL コードを Claude に書いてもらう例：

```
「Shader Graph の Custom Function ノードで使える
 Stylized Rim Light の HLSL コードを書いて。
 入力: Normal (Vector3), ViewDir (Vector3), RimPower (float)
 出力: Rim (float)」
```

出力例：
```hlsl
void StylizedRimLight_float(
    float3 Normal, float3 ViewDir, float RimPower,
    out float Rim)
{
    float rimDot = 1.0 - saturate(dot(Normal, ViewDir));
    Rim = pow(rimDot, RimPower);
    // ステップ関数でセル調に
    Rim = step(0.5, Rim);
}
```

---

## HLSL / Shader Code

`.hlsl` `.cginc` `.hlslinc` はテキストファイルなので Claude が直接書ける。

### よくある依頼パターン

```
「URP 対応の Unlit シェーダー（.hlsl）で、
 UV アニメーション付きのディゾルブ効果を実装して」
```

```
「このシェーダーコードをモバイル向けに最適化して。
 具体的にどこがパフォーマンスのボトルネックになっているか説明しながら修正して」
```

---

## UnityMCP と組み合わせた確認

制作しながら UnityMCP でリアルタイムに確認できる。

```
「今選択している GameObject のマテリアルの
 _EmissionColor の値を確認して、
 現在の値より 2倍明るくなる値を計算して」
```

```
「シーン内の全 Renderer が使っているシェーダーの一覧を出して。
 Standard シェーダーを使っているものがあれば教えて」
```
