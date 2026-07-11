# SUBGRADE 公開（デプロイ）ガイド

このサイトは**完全な静的サイト（HTML/CSS のみ）**です。ビルド不要で、そのまま無料ホストに置けば公開できます。

## 公開前チェックリスト
- [ ] `about.html` の運営者名・連絡先メールを記入
- [ ] 全ページの `href="#"`（X / note リンク）を実URLに差し替え
- [ ] `example.com` を実ドメインに一括置換（`robots.txt`・`sitemap.xml`・全HTMLの canonical / OGP / 構造化データ）
      例：`grep -rl example.com . | xargs sed -i '' 's#https://example.com#https://<あなたのドメイン>#g'`
- [ ] OGP画像 `assets/ogp.png`（1200×630）はそのまま利用可。差し替える場合も同サイズ推奨
- [ ] （AdSense承認後）各HTML `<head>` のローダー1行を有効化し、`ca-pub-XXXX`・`data-ad-slot` を記入
- [ ] （AdSense承認後）`ads.txt` をルートに設置：`google.com, pub-XXXXXXXXXXXXXXXX, DIRECT, f08c47fec0942fa0`

---

## 方法A：Netlify（ドラッグ&ドロップ・最速）
1. <https://app.netlify.com/drop> を開く
2. この `04_Webサイト` フォルダをブラウザにドラッグ&ドロップ
3. 数秒で `https://ランダム名.netlify.app` が発行される（独自ドメインも後から設定可）

## 方法B：Cloudflare Pages
1. Cloudflare にログイン → Workers & Pages → Create → Pages
2. 「Upload assets」で `04_Webサイト` の中身をアップロード（または Git 連携）
3. `https://プロジェクト名.pages.dev` で公開

## 方法C：GitHub Pages（Git運用したい人向け）
```bash
cd "04_Webサイト"
git init
git add .
git commit -m "SUBGRADE 初回公開"
# GitHubで空リポジトリを作成後：
git branch -M main
git remote add origin git@github.com:<ユーザー名>/<リポジトリ名>.git
git push -u origin main
```
その後、リポジトリの Settings → Pages → Source を `main / (root)` に設定。
`https://<ユーザー名>.github.io/<リポジトリ名>/` で公開されます。

> GitHub Pages を使う場合、ルートに空ファイル `.nojekyll` を置くと余計な処理を回避できます。

---

## 公開後にやること
- **Google Search Console** にサイト登録 → `sitemap.xml` を送信（インデックス促進）
- **AdSense** に公開URLで申請 → 承認後に広告コードを有効化
- note / X から記事へ流入導線をつくる
