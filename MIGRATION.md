# 移行手順（Claude Code on the web セッションで実行）

このtarballには**18ファイル**が入っている。
Drive にあった残り6ファイルは含まれていないので、下記手順で合流させる。

---

## 手順

### 1. このtarballを展開

```bash
tar -xzf softskills-wiki.tar.gz --strip-components=1
```

### 2. Drive の残り6ファイルを合流させる

Google Drive「ソフトスキルWiki」フォルダを**ZIPでダウンロード**し、
このセッションに添付して展開する。以下**6ファイルだけ**をコピーする。

```
frameworks/日本のフレームワーク.md
concepts/ソフトとハードの境界.md
concepts/自己申告の限界.md
sources/主要文献リスト.md
sources/文献取得ガイド.md
analyses/日常語からの逆引き.md
raw/2026-09-10_対話ログ_ソフトスキル体系化.md
```

**Drive 側を採用してはいけないファイル**（このtarball側が新しい）：

```
AGENTS.md（SCHEMA.md を置き換え。Drive の SCHEMA.md は破棄）
index.md  log.md  overview.md
frameworks/BESSI.md  frameworks/地図の余白.md
concepts/136フレームワーク問題.md  concepts/コミュニケーションコスト.md
concepts/信頼と特異性クレジット.md  concepts/訓練可能性L1-L5.md
concepts/専門職化の4条件.md  concepts/特性とスキル習得.md
skills/37スキル一覧.md
sources/BESSI原典_WorldBank報告書.md（新規）  sources/要確認リスト.md
inbox/ の5ファイル（統合済み。破棄）
```

### 3. Drive 由来のエスケープを直す

Drive コネクタ経由で書いたファイルは `\#\#` `\*\*` `\[\[` のようにエスケープされている。

```bash
# 確認
grep -rl '\\#\\#' . 2>/dev/null

# 一括修正
find . -name '*.md' -exec sed -i 's/\\\([#*\[\]_>-]\)/\1/g' {} +
```

### 4. リンク切れチェック

```bash
grep -oh '\[\[[^]]*\]\]' -r . | sort -u | tr -d '[]' | while read p; do
  find . -name "$p.md" | grep -q . || echo "MISSING: $p"
done
```

`SCHEMA` へのリンクが残っていたら `AGENTS.md` を指すよう直す（本文からの参照は
バッククォート表記に変えてあるので、出るとしたら Drive 由来の6ファイル）。

### 5. コミットしてPR

```bash
git add .
git commit -m "Drive→GitHub移行 + BESSI原典ingest + inbox5件統合

- 統合コストが1ページ2コールから1操作に
- SCHEMA.md → AGENTS.md（Git運用の節を追加）
- ★二重訂正：間隙的ファセット4つは誤りではなかった（原典で確認）
- World Bank技術報告書をingest、sources/ に要約ページ新規
- 7層モデル（認知能力・知識を追加）
- 知識の呪い／メタ認知律速段階／レジリエンス三層を反映"
```

---

## 完了後

1. **Google Drive コネクタを外す**（Claudeの設定から）
2. Drive フォルダは `_archive_20260927` にリネームして1〜2週間残す
3. Claude Project のカスタム指示から Drive 固有の記述を削除。`AGENTS.md` があるので指示は最小限でよい

## 今後の運用

- スマホから claude.ai/code でセッションを起動
- 「統合」「lint」「拾って」の短縮コマンドは `AGENTS.md` に定義済み
- Obsidian で vault として開けば `[[ ]]` が機能し、グラフビューで孤立ページを視認できる
