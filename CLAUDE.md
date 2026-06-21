# CLAUDE.md

このファイルは、このリポジトリで作業する AI アシスタント（Claude Code など）向けのガイドです。

## プロジェクト概要

美容サロンオーナー向けの集客コンサルティング事業（ブランド名: **RAI / HPB Consultant** および **Salon Result Lab**）の **静的 Web サイト一式**です。HPB（ホットペッパービューティー）・minimo・Google マップ・Instagram・Threads などの集客ノウハウを、LP（ランディングページ）・ノウハウ記事・無料特典・分析ツールとして配信します。

- **言語**: ページ内容はすべて日本語（`<html lang="ja">`）
- **技術スタック**: 素の HTML + CSS のみ。ビルドツール・パッケージマネージャ・JS フレームワークは**一切なし**（`package.json` も存在しない）
- **JavaScript**: 一部のページのみ、外部依存のないバニラ JS を `<script>` インラインで使用（分析ツール、LP のスティッキー CTA など）
- **動かし方**: ブラウザで `.html` を直接開くだけ。ビルド・サーバー・依存インストールは不要

## ディレクトリ構成

```
/
├── index.html              無料プレゼント10選のハブページ（RAIブランド）
├── lp.html                 メインLP「HPB×SEO完全攻略ガイド／10大特典」（RAIブランド）
├── line-lp.html            LINE登録用LP「7大特典＋無料HPB診断」（自己完結スタイル）
├── 01.html 〜 10.html      10大特典の各ノウハウ記事（RAIブランド、style-light.css使用）
├── 7gifts.html             7大特典ページ（Salon Result Labブランド）
├── blog-auto.html          ブログ＆フォトギャラリー自動化サービス提案ページ
├── minimo-guide.html       minimo集客 完全攻略ガイド（9章＋40項目チェックリスト）
├── style-light.css         ライト＆ゴールドのメインテーマ（index/lp/01〜10で共有）
├── style.css               ダークテーマ（旧版・現在どのHTMLからも未参照／レガシー）
├── gifts/                  自己完結型の特典7本（gift-style.css を共有）
│   ├── 01-hpb-checklist.html      HPB集客改善チェックリスト
│   ├── 02-minimo-guide.html       minimo集客スタートガイド
│   ├── 03-google-map.html         Googleマップ集客セットアップシート
│   ├── 04-instagram-template.html Instagram投稿テンプレ7日分
│   ├── 05-chatgpt-prompts.html    サロン向けChatGPTプロンプト集
│   ├── 06-set-menu.html           客単価UPセットメニュー設計テンプレ
│   ├── 07-counseling-sheet.html   新規リピート率UPカウンセリングシート
│   └── gift-style.css             gifts/ 配下共通のスタイル
├── hpb-report-analyzer/    HPBサロンレポート分析ツール（貼り付け→分析の静的HTML）
│   └── index.html
├── threads-post-analyzer/  Threads投稿分析ツール（README付き、貼り付け→分析）
│   ├── index.html
│   └── README.md           入力カラム仕様・判定ロジックの説明
├── threads-daily-posts/    日付別のThreads投稿原稿置き場
│   └── 2026-05-26/index.html
└── images/                 画像（style-photo.jpg / .webp）
```

## ページの2つのブランド系統

このサイトには時期の異なる **2つのデザイン系統**が混在しています。新規ページや編集時は、対象ファイルがどちらに属するか確認してから合わせてください。

1. **RAI / HPB Consultant 系（旧／ゴールド・ライトテーマ）**
   - 対象: `index.html`, `lp.html`, `01.html`〜`10.html`
   - スタイル: 外部 `style-light.css` を `<link>` で参照（CSS 変数で色を統一）
   - フォント: `Noto Sans JP`、アクセントに `Bebas` 系

2. **Salon Result Lab 系（新／自己完結スタイル）**
   - 対象: `7gifts.html`, `blog-auto.html`, `minimo-guide.html`, `line-lp.html`, `gifts/*.html`
   - スタイル: 各ファイルに `<style>` をインラインで持つ自己完結型（`gifts/` だけは共通の `gift-style.css`）
   - 配色: オレンジ系のグラデーション（`#FF8C42`→`#E85D10` など）

## スタイリングの規約

- **CSS 変数を使う**: `style-light.css` の `:root` に色・影・角丸が定義済み。新しい色をハードコードせず既存変数を再利用する。
  - 例: `--gold:#C9932A`, `--text:#1A1A2E`, `--line-green:#06C755`, `--green:#059669`, `--radius:12px`, `--shadow` など
- **`style.css`（ダークテーマ）は現在どのページからも参照されていないレガシーファイル**。これに依存・編集する前に、本当に使われているか必ず確認すること。安易に他ページへ適用しない。
- BEM 風のクラス命名（`hero__badge`, `site-header__inner` など）を踏襲する。
- モバイルファースト。`<meta name="viewport">` 必須、レイアウトはスマホ表示を主眼に確認する。

## CTA / 外部リンクの規約（重要）

集客サイトのため、CTA（行動喚起）リンクが最重要要素です。**URL を勝手に変更・捏造しない**こと。既存ページから現行の値をコピーして使う。

- **LINE 登録リンク**: `https://lin.ee/...` 形式（ページ・キャンペーンごとに複数の LINE アカウントが使い分けられている。例: `lin.ee/usQ5jomD`, `lin.ee/UbEyJAu`, `lin.ee/nsMovyr`）。どのリンクを使うかは編集対象ページの既存値に従う。
- **無料相談予約（TimeRex）**: `https://timerex.net/s/tattoou123456_ad67/57c1cebf`
- CTA は「導入相談予約（TimeRex）」と「LINE で相談」の2導線が基本構成。新規 CTA を作る際はこの2導線パターンに揃える。

## 開発ワークフロー

- **ビルド不要**: HTML/CSS を編集し、ブラウザで該当 `.html` を開いて目視確認する。
- ローカル確認が必要なら任意の静的サーバ（例: `python3 -m http.server`）でルートから配信できる。リンクはルート相対／相対パス前提。
- **テストフレームワークは無し**。検証は「ブラウザで開いて表示・リンク・レスポンシブを確認」が基本。
- 価格・実績数値などは事実情報。**数値（料金・PV実績・割合）を推測で変更しない**。変更指示があった場合のみ、全関連ページで表記を統一する（税込表記・実績数値は過去にページ横断で揃えた経緯あり）。

## Git / コミット規約

- **作業ブランチ**: `claude/claude-md-docs-f31ak4`（このタスクの指定ブランチ）。`main` へ直接プッシュしない。
- **コミットメッセージは日本語**。リポジトリの慣習に従い、「何を・なぜ変えたか」を簡潔に記述する。
  - 例: `CTAを導入相談予約(TimeRex)＋LINEで相談の2導線に整理`
  - 例: `PV実績を5000→16000に変更、税込価格に統一`
- プッシュは `git push -u origin <branch-name>`。ネットワーク失敗時のみ指数バックオフ（2s/4s/8s/16s）で最大4回リトライ。
- **プルリクエストはユーザーから明示的に依頼された場合のみ作成**する。

## 編集時の注意点

- 各 HTML はほぼ独立したページで、共有されるのは `style-light.css` / `gift-style.css` のみ。CSS を変更する場合は**参照している全ページへの影響**を確認する。
- 画像は WebP を優先（`images/` には `.jpg` と `.webp` の両方があり、過去に「中身が WebP なのに拡張子が誤り」を修正した経緯あり）。拡張子と実体の整合に注意。
- 分析ツール（`hpb-report-analyzer/`, `threads-post-analyzer/`）はバニラ JS の自己完結ツール。`threads-post-analyzer/README.md` に入力カラム仕様と判定ロジック（反応率・CTA率・LINE転換率・相談転換率の定義）があるので、ロジック変更時は README も更新する。
