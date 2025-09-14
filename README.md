# Corporate Website Template

静的なコーポレートサイトのテンプレートです。ヒーローエリア（スライダーの想定）、カード型のサービス一覧、ニュース、料金表、Google マップのアクセス、問い合わせフォームで構成されています。

## 技術スタック

- 言語: HTML5 / CSS3 / Vanilla JavaScript
- ライブラリ: Swiper 4.5.0（`js/swiper.js`）、WOW.js（`js/wow.min.js`）、Animate.css（`CSS/animate.css`）
- スタイル: カスタム CSS（`CSS/styles.css`）、Swiper 用スタイル（`CSS/swiper.css`）
- インフラ・CI: なし（`.github/workflows` 等は未配置）

## 主な機能

- ヒーローセクション: `.swiper-container` ベースのスライダー用 DOM 構造と前後ボタン・ページネーション
- サービス/製品（Card）: カード型レイアウトでタイトル・テキストの一覧
- ニュース: 日付・ラベル・本文のリスト表示
- 料金（Price）: テーブル形式の料金比較＋補足注記
- アクセス（Access）: Google マップの `iframe` 埋め込み＋住所/アクセス表、地図へのリンク
- 問い合わせ（Contact）: 入力フォーム（名前/メール/種別/内容/ラジオ）と送信ボタン（静的）

## 設計・実装の工夫

- スクロールアニメーション: WOW.js（`new WOW().init()`）で見出しや要素をアニメーション表示
- セクション設計: `id` に基づくアンカーナビゲーション（ヘッダー/フッターのメニュー）
- 依存の自己完結: Swiper/WOW/Animate.css をローカルに同梱し、外部 CDN に依存しない構成

## セットアップ & 動作確認

ローカルで動作する静的サイトです。ビルド手順は不要です。

1) ブラウザで開く（最小手順）
- `index.html` をダブルクリック、またはブラウザで開くだけで表示されます。

2) 静的サーバで配信（推奨）
- Python: `python3 -m http.server 8000` を実行し、`http://localhost:8000/` を開く
- Node.js（任意）: 任意の静的サーバ（例: `npx http-server` など）でも可

## 改善ポイント / TODO（リポジトリからの事実に基づく）

以下は、ソースコード・ディレクトリ構成・設定ファイル・コメントから読み取れる事実に基づく改善候補です。

### 機能
- スライダー初期化: `index.html` に Swiper 初期化コードがありません（`new Swiper('.swiper-container', { ... })` の追加が必要）。
- 問い合わせフォーム: `action`/`method` が未設定で、実送信はできません。

### HTML / アクセシビリティ
- 代替テキスト: `img` に `alt` 属性がほぼ未設定。
- 重複 ID: `id="item"` が複数箇所で重複しており、仕様違反かつスクリプト連携の障害になりえます。
- 役割の適合: 送信ボタンが `div` 要素（`#contact-button`）であり、キーボード操作/ARIA 的に不十分。`button` へ変更推奨。
- ラベルと入力の対応: `label for` と `input id` の組み合わせや `name` 属性が未整備。
- 言語/メタ: `<html>` に `lang` がありません。`<meta name="description">` などの SEO メタや `<meta name="viewport">` も未設定。

### レスポンシブ / デザイン
- 固定幅: 多くのブロックが `width: 1366px` 固定でメディアクエリも未定義。レスポンシブ対応が未実装。

### パフォーマンス
- 画像最適化: 画像の最適化状況は不明（WebP/AVIF などの軽量化や `width/height` 明示）。
- アセット最適化: `swiper.js` は非 minified、CSS/JS の結合・縮小は未実施。
- 不要ファイル: `.DS_Store` がコミットされています。`.gitignore` で除外推奨。

### SEO
- メタ情報: `title` 以外の主要メタ（`description`/OGP/Twitter Card）未設定。
- 見出し構造: `h1` が複数あるためページのアウトライン見直し余地あり。

### テスト / 品質
- 自動テスト: ユニットテスト/E2E テストは未整備。
- 品質チェック: Lint/Formatter/アクセシビリティチェック/Lighthouse などの自動化は未整備。

### CI/CD
- CI: `.github/workflows` 等の CI 設定はありません。ビルド不要の静的サイトでもリンク切れや Lint を自動化可能です。

### ドキュメント
- カスタマイズ手順: セクションの追加・スライダー設定・フォーム接続の手順が未記載。

## 強調したいポイント（本リポジトリで示しているスキル）

- ローカル配布のライブラリを組み合わせた、自己完結型の静的サイト構成
- WOW.js/Animate.css による視覚効果の導入
- セクション分割とアンカーナビに基づくシンプルな情報設計

---

### 参考: Swiper の初期化例

```html
<script>
  var swiper = new Swiper('.swiper-container', {
    loop: true,
    pagination: { el: '.swiper-pagination', clickable: true },
    navigation: { nextEl: '.swiper-button-next', prevEl: '.swiper-button-prev' },
  });
  new WOW().init();
\n</script>
```
