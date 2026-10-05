# sudoh.nl — Hugo

研究者の個人サイトをGoogle SitesからHugoへ移行するための構築基盤です。
元サイトの本文と、ご提供いただいたプロフィール写真を移行済みです。
詳細と所属表記の確認事項は [移行記録](docs/migration.md) を参照してください。

## 開発

Hugo 0.147.9（通常版）を使用します。テーマはPaperModで、ソースを同梱しています。

```sh
hugo server --bind 0.0.0.0 --port 1313
hugo --gc --minify
```

本文は `content/`、画像やPDFは `static/`、サイト設定は `hugo.toml` に置きます。
元サイトの英語本文、外部リンク、旧見出しIDを保持し、`/home/` をホームに転送します。
研究業績や連絡先は元サイトの表記に合わせています。

## 英語版・日本語版

初期表示は英語（`/`）で、日本語版は `/ja/` です。
ヘッダーの「日本語」「English」リンクで切り替えられます。
ブラウザーの言語設定による自動転送は行いません。

英語本文は `content/_index.md`、日本語本文は `content/_index.ja.md` にあります。
内容を更新するときは両方を編集し、対応する見出しのIDを一致させてください。
目次・写真の代替テキストは `i18n/`、言語ごとのメニューは `hugo.toml` に設定します。
英語で発表された論文のタイトルは日本語版でも原題を保持しています。

アカウント一覧のリンク先と英語・日本語の表示名は `data/social_accounts.yaml` で管理します。
両言語の本文で `social-accounts` ショートコードを使い、PaperMod同梱のSVGロゴを表示します。
一覧のスタイルは `assets/css/extended/social-accounts.css` にあります。

レイアウトはPaperModのまま、`assets/css/extended/slc-colors.css` で配色を調整しています。
研究室の[公式公開リポジトリ](https://github.com/nara-wu-slc/nara-wu-slc.github.io)
のCSSにあるオリーブグリーン（`#99ab4e`）を基準にし、文字には読みやすい濃淡を使用します。
ダークモードにも対応しています。

`disablePathToLower = true` は、旧見出しIDの大文字をメニューURLでも保持するために必要です。

## GitHub Pages

本文の移行と確認後、リポジトリのSettings → PagesでSourceをGitHub Actionsに設定し、
Actionsの「Deploy Hugo to GitHub Pages」を手動実行します。
現在は公開のタイミングを選べるよう、pushによる自動公開を有効にしていません。
GitHub Pages側で独自ドメイン `www.sudoh.nl` とHTTPSを設定してください。
DNS切替は新サイトの確認後に行ってください。この作業ではDNS変更や公開は行っていません。
ビルド時のbaseURLはGitHub Pagesの設定に合わせて上書きされます。

## テーマ

[PaperMod](https://github.com/adityatelange/hugo-PaperMod)
のコミット `d3768854d00ad003b0a8dbdba254ce9224377a01` を同梱。
MITライセンスは `themes/PaperMod/LICENSE` に保存しています。
