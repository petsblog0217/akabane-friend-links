# CLAUDE.md — akabane-friend-links（採用リンクページ）

## §0 母艦ポインタ
- このプロジェクトは **agent-ops（母艦）が束ねる案件レイヤーの1案件**です。
- 全社共通ルール（コア＋playbook）と母艦の文脈が常に上位：`~/.claude/CLAUDE.md`（= agent-ops `docs/global/_core.md`）を最初に読むこと。
- 案件カード：agent-ops `docs/projects/akabane-friend-links.md`
- 優先順位は ADR-003（ハイブリッド）準拠。§1キャラ・§2ツール実行前確認・§6セキュリティは案件でも覆せない下限。

---

## 1. このプロジェクトは何か
**赤羽歯科・フレンドデンタルオフィス**の採用用「リンクまとめページ」（lit.link のような1枚もの）。
パンフレットに **QRコード**で載せ、スマホで開いてもらう前提。紹介動画（YouTube・限定公開）・法人HP・採用サイトへ誘導する。

## 2. 構成
- `index.html` … 歯科衛生士 向けページ（動画2本：寮紹介／業務紹介）
- `reception.html` … 受付・歯科助手 向けページ（動画3本：寮紹介／受付業務／歯科助手業務）
- `images/` … ロゴ2点（logo-akabane.png / logo-friend.png）
- `make_qr.py` … QRコード生成スクリプト（※QR画像と本スクリプトは **リポジトリに含めない** 方針＝CEO判断。手元の `qr/` にのみ保存）

## 3. 公開（GitHub Pages）
- リポジトリ：**petsblog0217/akabane-friend-links（public）** ※Pages無料利用のため公開。中身は公開前提の採用ページ。
- 公開URL：
  - 歯科衛生士：https://petsblog0217.github.io/akabane-friend-links/
  - 受付・歯科助手：https://petsblog0217.github.io/akabane-friend-links/reception.html
- 反映：`main` に push → GitHub Pages が自動再ビルド（1〜2分）。

## 4. デザイン
- パステル（ミント×クリーム×淡ピンク）、丸ゴシック（Zen Maru Gothic）。可愛い×清潔感×誠実シンプル。
- スマホ最適化（QR前提）。色は `index.html` の `:root` 変数で一括変更可。

## 5. 編集のしかた
- **普段は Claude に「ここ直して」と頼むのが確実**（編集→push→自動反映まで一括）。
- 自分で直す場合は、ブラウザで github.com に `petsblog0217` でログインしてからファイルを編集（ログインしていないと読み取り専用）。動画URLは各 `<iframe ... /embed/○○○>` の `○○○`（動画ID）を差し替え。コメントで差し替え箇所を明示済み。

## 6. つまづき・注意（重要）
- **YouTube限定公開の埋め込み**：限定公開でも「埋め込みを許可」がONなら埋め込み可。ただし **`file://`（ファイル直開き）だと埋め込みがブロックされ「設定エラー」になる**。`http://`（ローカルサーバ）か本番httpsでは正常に再生される。確認は `python -m http.server` か本番URLで。
- **採用ボタン文言**：「問い合わせ」表記で統一（「お問合せ」ではない＝CEO選択）。
- QRは誤り訂正レベルH・余白4マスで生成（印刷の汚れ・反射に強い）。
