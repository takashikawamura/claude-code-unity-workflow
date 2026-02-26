# 10. テスト方法

## テスト方法の比較

| 方法 | 特徴 | 向いているケース |
|---|---|---|
| **ローカル（Claude）で TestRunner を実行** | 最もシンプル | 日常的な開発 |
| Unity Build Automation | ビルドごとにテスト、セットアップが軽い | シンプルな CI が欲しいとき |
| GitHub Actions + GameCI | テストだけのジョブを組める、セットアップが重い | 本格的な CI を組みたいとき |

---

## ローカルでの TestRunner 実行

スキル: `/test-unity`

Claude が Unity TestRunner を呼び出してテストを実行する。

### EditorMode vs PlayMode

| モード | 特徴 | 使いどころ |
|---|---|---|
| **EditorMode** | MonoBehaviour 不要、高速 | ロジック・ユーティリティのテスト |
| **PlayMode** | ゲーム実行状態をシミュレート | MonoBehaviour を含むテスト |

---

## Unity Build Automation

ビルドごとにテストが走る。セットアップが軽くシンプル。

参考: https://yurinchi2525.com/build-automation/

---

## GitHub Actions + GameCI

テストだけのジョブを組める本格的な CI。セットアップが重い。

参考: https://www.hanachiru-blog.com/entry/2024/02/26/120000
