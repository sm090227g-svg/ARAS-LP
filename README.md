# ARASウェブサイト（aras0099.netlify.app）

## ① 今後の更新方法（Git連携版）

これまでNetlifyに直接ドラッグ&ドロップしてたけど、これからは
**このリポジトリにpushするだけで自動的にサイトが更新される**ようになるで。

```
git add .
git commit -m "ブログ記事を追加"
git push
```

これだけでOK。Netlify側の設定は下の「② セットアップ手順」で一度だけやればええ。

## ② セットアップ手順（最初の1回だけ）

### GitHubにリポジトリを作る
1. https://github.com/new で新規リポジトリ作成（例: `aras-website`）
2. Public/Privateどちらでも可（Privateでも次のNetlify連携は無料でできる）
3. ローカルのこのフォルダをpush
   ```
   cd aras-website
   git init
   git add .
   git commit -m "initial commit"
   git branch -M main
   git remote add origin https://github.com/(あなたのユーザー名)/aras-website.git
   git push -u origin main
   ```

### Netlifyとリポジトリを連携する
1. https://app.netlify.com/projects/aras0099/configuration/deploys を開く
2. 「Link repository」または「Build & deploy」→「Link site to Git」を選択
3. GitHubを選び、認可 → 先ほど作った `aras-website` リポジトリを選択
4. Build command は空欄のまま、Publish directory は `.`（ルート）を指定
5. 「Deploy site」

これで以後、`git push` するたびに自動でNetlifyに反映されるようになる。

## ③ ブログ記事の追加方法

1. `blog/_template.html` をコピーして、`blog/posts/新しいファイル名.html` として保存
   - ファイル名は英数字とハイフンのみ。地域名+症状などをローマ字で入れるとSEOに強い
     例: `ikeda-gaiheki-tosou-jiki.html`
2. テンプレート内の【　】部分を実際の内容に書き換える
3. `blog/index.html` の記事一覧（`<main class="blog-list">` の中）に、新しい記事へのリンクカードを追加
4. `git add . && git commit -m "記事追加" && git push`

## ④ ディレクトリ構成

```
aras-website/
├── index.html          … トップページ（LP）
├── blog/
│   ├── index.html       … ブログ記事一覧ページ
│   ├── _template.html   … 新規記事作成用テンプレート
│   └── posts/
│       ├── kawanishi-gaiheki-hibiware-genin-taisho.html
│       └── takarazuka-yane-tosou-hiyou-souba.html
└── README.md
```

## ⑤ SEOのポイント（運用時に意識すること）

- タイトル・meta descriptionには必ず地域名（川西・宝塚・池田）＋具体的なキーワードを入れる
- 記事は週1〜隔週ペースでの継続更新を目指す（質を優先、無理のない頻度で）
- 記事公開後は Google Search Console でインデックス登録をリクエストする
- 記事同士を「あわせて読みたい」で内部リンクし、サイト内の回遊性を高める
