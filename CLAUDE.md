# CLAUDE.md

このファイルはリポジトリでの作業時に Claude Code (claude.ai/code) へのガイダンスを提供します。

## コマンド

```bash
pnpm dev          # 開発サーバー起動
pnpm build        # 静的サイトのビルド
pnpm preview      # 本番ビルドのプレビュー
pnpm check        # svelte-check による型チェック
pnpm lint         # ESLint
pnpm format       # Prettier
```

## アーキテクチャ

**SvelteKit + static adapter** による個人ポートフォリオ/ブログ（全ページ事前レンダリング）。全体を通じて **Svelte 5 runes** 構文を使用。

**主要パス:**
- `src/routes/` — ファイルベースルーティング: `/`, `/bio`, `/blog`, `/blog/[slug]`
- `src/components/` — 共有 Svelte コンポーネント (Nav, Button, Profile, Social, LargeTitle)
- `src/lib/blog/index.ts` — ブログユーティリティ: `getPosts()` と `getPost(slug)`（マークダウン処理パイプライン含む）
- `src/content/blog/*.md` — YAML frontmatter 付きブログ記事 (`title`, `description`, `date`, `published`, `tags`)

**スタイリング:** Wind3 プリセット付き UnoCSS。HTML 要素に `class="..."` または `uno="..."` 属性を直接使用。カスタムショートカットは `uno.config.ts` で定義（`fcc`, `fcol` 等のフレックス/グリッドヘルパー、ボタン用 `btn-{color}`）。

**マークダウン処理パイプライン** (`src/lib/blog/index.ts`): `gray-matter` → `remark-parse` → `remark-rehype` → `rehype-pretty-code` (Shiki, `github-dark` テーマ) → `rehype-slug` → `rehype-autolink-headings` → `rehype-stringify`。

**ダークモード:** `svelte-fancy-darkmode`。ダーク専用スタイルは `html.dark` セレクターを使用。テーマカラー: ダーク `#0F0F0F`、ライト `#ffffff`。

**View Transitions API:** `+layout.svelte` 内の `document.startViewTransition()` でナビゲーションをラップ。名前付きトランジションには要素に `view-transition-name` を使用。

**アニメーション:** `prefers-reduced-motion` 対応の CSS キーフレームアニメーション。初回訪問時の単語ごとの段階的アニメーションは `sessionStorage` に保存。

**ブログ記事:** `published: true` の記事のみ表示。`date` の新しい順にソート。

**パスエイリアス:** `$components` → `src/components/`（`svelte.config.js` で設定）。

**SEO:** OpenGraph/Twitter メタ用に `svelte-meta-tags` を使用。タイトルテンプレート: `{title} | irom999.com`。

**言語:** `app.html` に `lang="ja"`。一部コンテンツは日本語。
