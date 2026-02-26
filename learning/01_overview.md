# 01. 前提・環境・必要ツール

## 対象環境

- OS: Windows
- Unity: Unity 6

## 必須ツール

| ツール | 役割 |
|---|---|
| **ClaudeCode** | AI コーディングアシスタント（メイン） |
| **GitHub CLI** | Issue・PR・ブランチ操作を CLI から行う |
| **UnityMCP** | Claude から Unity Editor を操作するための MCP サーバー |

## 各ツールの関係

```
ClaudeCode
  ├── GitHub CLI  → Issue作成 / PR作成 / レビュー対応
  └── UnityMCP    → UnityEditor の操作・確認
```

## 注意

このワークフローは 2025/02 時点のものであり、今後変わる可能性がある。

## 確認ポイント

- [ ] ClaudeCode がインストールされているか
- [ ] GitHub CLI (`gh`) がインストールされ、認証済みか
- [ ] UnityMCP が Unity プロジェクトに導入されているか
