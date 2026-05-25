# Cloudflare でサイトが更新されないとき

GitHub の `main` は最新でも、Cloudflare 側が **別ブランチ** や **初回デプロイのまま** だとサイトは古いままです。

## 1. 本番ブランチを `main` にする（Git 連携の場合）

1. [Cloudflare ダッシュボード](https://dash.cloudflare.com/) → **Workers & Pages** → プロジェクト **kanben**
2. **Settings** → **Builds**（または Builds & deployments）
3. **Production branch** を **`main`** に変更（`cloudflare/workers-autoconfig` になっていないか確認）
4. **Retry deployment** / **Create deployment** で再デプロイ

## 2. GitHub Actions でデプロイする（推奨・確実）

1. Cloudflare で API トークンを作成（**Edit Cloudflare Workers** テンプレート）
2. GitHub リポジトリ → **Settings** → **Secrets and variables** → **Actions**
3. 次を追加:
   - `CLOUDFLARE_API_TOKEN`
   - `CLOUDFLARE_ACCOUNT_ID`（ダッシュボード右側の Account ID）
4. **Actions** タブ → **Deploy to Cloudflare** → **Run workflow**

`main` に push するたびに自動デプロイされます。

## 3. ブラウザのキャッシュ

- サイトを **スーパーリロード**（Ctrl+Shift+R）
- ページのソース表示で `<meta name="app-build"` の値が最新か確認

## 4. 正しい URL

ルートの **`/`**（`index.html`）を開いてください。古いブックマークの `/kanben.html` だけが古い場合があります。
