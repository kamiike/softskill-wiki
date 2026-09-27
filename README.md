# ソフトスキル体系化 — LLM Wiki

ソフトスキルを体系化するための知識ベース。
[Karpathy の LLM Wiki パターン](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) に基づく。

## 使い方

```bash
# Claude Code で開く
cd softskills-wiki && claude
```

`AGENTS.md` が規範。LLMはセッション開始時に `index.md` と `log.md` を読む。

## 構造

```
.
├── AGENTS.md      規範（LLMへの設定ファイル）
├── index.md       全ページのカタログ
├── log.md         操作の時系列記録（追記のみ）
├── overview.md    プロジェクト全体像
├── raw/           原資料（人間が所有。LLMは読むだけ）
├── inbox/         未統合の断片（一時領域）
├── frameworks/    既存の枠組み
├── concepts/      本プロジェクト独自の概念
├── skills/        37スキル
├── sources/       文献の要約
└── analyses/      比較・統合
```

## 記号

| 記号 | 意味 |
|---|---|
| ◆ | 本プロジェクト独自の主張。既存文献に対応物がない |
| ▲ | 推定・論理的推論。実証データなし |
| 【要確認】 | 原典未確認 |

**この3記号は絶対に落とさない。**本プロジェクトの信頼性は、どこが実証でどこが推定かを区別できることに依存している。

## Obsidian

このリポジトリはそのまま Obsidian の vault として開ける。
`[[ページ名]]` 記法が機能し、グラフビューで関連を追える。
