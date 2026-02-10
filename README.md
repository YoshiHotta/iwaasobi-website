# iwaasobi-website

イワアソビ公式サイト。GitHub Pages + Jekyll でホスティング。

公開URL: https://iwaasobi.com

## ページ一覧

| ページ | パス | ファイル |
|---|---|---|
| LP | `/` | `index.md` |
| プライバシーポリシー | `/privacy-policy` | `privacy-policy.md` |
| 利用規約 | `/terms` | `terms.md` |
| FAQ | `/faq` | `faq.md` |

## 技術構成

- **Jekyll** — 静的サイトジェネレーター。Markdown を HTML に変換する
- **GitHub Pages** — main ブランチに push すると自動でビルド・デプロイされる
- **SCSS** — CSS のプリプロセッサ。`_sass/` 配下のファイルで管理

### 用語

**bundle** — Ruby のパッケージマネージャ。`Gemfile` に書かれた依存ライブラリ（Jekyll 本体と GitHub Pages 関連の gem）をインストール・管理する。Flutter でいう `pub get` と `fvm flutter run` に相当。

**WebView** — アプリ内にブラウザを埋め込んで Web ページを表示する仕組み。Flutter アプリから URL を開くと、アプリ画面内にそのページが表示される。`?webview=true` パラメータ付きで開くと、ヘッダー・フッターが非表示になり、コンテンツのみが表示される（アプリ自体のナビゲーションと二重になるのを防ぐため）。

## ディレクトリ構成

```
iwaasobi-website/
├── CNAME                    # カスタムドメイン設定 (iwaasobi.com)
├── _config.yml              # Jekyll 設定
├── _layouts/
│   └── default.html         # 共通レイアウト (header/footer/nav + WebView対応JS)
├── _includes/
│   ├── header.html          # サイトヘッダー・ナビゲーション
│   └── footer.html          # サイトフッター
├── _sass/
│   ├── _base.scss           # ベーススタイル・リセット
│   ├── _layout.scss         # レイアウト・レスポンシブ対応
│   └── _webview.scss        # WebView 用スタイル (ヘッダー/フッター非表示)
├── assets/
│   ├── css/
│   │   └── style.scss       # SCSS エントリーポイント
│   └── images/
│       └── logo.jpeg        # ロゴ
├── index.md                 # LP
├── privacy-policy.md        # プライバシーポリシー
├── terms.md                 # 利用規約
├── faq.md                   # FAQ
└── Gemfile                  # Ruby 依存関係定義
```

## セットアップ（初回のみ）

```bash
cd iwaasobi-website
bundle install
```

## コンテンツ更新手順

### 1. feature ブランチを作成

```bash
git checkout main
git pull origin main
git checkout -b update-faq   # ブランチ名は作業内容に合わせる
```

### 2. Markdown ファイルを編集

対象の `.md` ファイルを直接編集する。

### 3. ローカルで確認

```bash
bundle exec jekyll serve
```

ブラウザで http://127.0.0.1:4000/ を開いて確認。ファイルを保存すると自動で再ビルドされるので、ブラウザをリロードするだけで反映される。

WebView モードの確認は URL に `?webview=true` を付ける（例: http://127.0.0.1:4000/faq?webview=true ）。

確認が終わったら `Ctrl+C` でサーバーを停止。

### 4. commit して push

```bash
git add .
git commit -m "FAQを更新"
git push origin update-faq
```

### 5. PR を作成して merge

GitHub 上で Pull Request を作成し、確認後 main に merge する。merge すると GitHub Pages が自動でビルド・デプロイする（反映は数分以内）。

## WebView 対応

Flutter アプリ内の WebView からは `?webview=true` パラメータを付けて開く。

| 表示方法 | URL例 | ヘッダー/フッター |
|---|---|---|
| ブラウザで直接 | `https://iwaasobi.com/faq` | 表示される |
| アプリ内 WebView | `https://iwaasobi.com/faq?webview=true` | 非表示 |

## FAQ アンカーリンク

FAQ の各質問には ID が付いており、直接リンクできる。メールでの問い合わせ対応時に特定の質問へ誘導する際に使う。

例: `https://iwaasobi.com/faq#forgot-password`
