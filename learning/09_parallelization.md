# 09. Unity 開発の並列化

## 結論

**Unity の特性上、並列化は相性が悪い。**

---

## Git Worktree

ローカルリポジトリで作業ツリーを複数同時に持てる仕組みだが、Unity との相性が悪い。

### 問題点

| 問題 | 詳細 |
|---|---|
| Library フォルダ | worktree ごとに再生成が必要（数分〜数十分） |
| Unity Editor | 1プロジェクト = 1エディタインスタンスが原則 |
| MCP 接続 | Unity エディタ 1つにつき 1接続 |
| シーン/Prefab | バイナリ的でマージコンフリクトしやすい |

---

## Agent Teams（部分的に有効）

`TeamCreate` で複数エージェントが同一リポジトリ内で並列作業できる。

### 有効なケース

Unity MCP が不要な `.cs` ファイルの作業なら衝突しにくい：

```
エージェントA → UserProfile.cs, ChatMessage.cs
エージェントB → AuthUseCase.cs, LobbyUseCase.cs
```

### 運用パターン

1. メインコンテキストが UnityMCP を使い Unity Editor を操作する
2. Agent Teams で `.cs` を並列実装する
3. メインセッションで MCP 確認・テストを行う

---

## 物理的に PC を用意する

Unity + Git + Claude を入れた PC を複数用意して、遠隔またはローカルで同時に作業する方法もある。

---

## まとめ

| 方法 | 実用性 |
|---|---|
| Git Worktree | 相性が悪い（非推奨） |
| Agent Teams（.cs のみ） | 部分的に有効 |
| 複数 PC | 物理的コストがかかるが有効 |
