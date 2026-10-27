# tsumugitomarimo.com 運用マニュアル

株式会社TSUMUGI TO MARIMO のコーポレートサイトの「設計図と取扱説明書」です。
HPに問題が起きたとき、またはAI（Claude など）や制作者に作業を頼むときは、まずこのファイルを読ませてください。

- 最終更新：2026年10月28日
- 作成：Claude（古閑さんとの作業記録をもとに作成）
- パスワード類はここには書いていません。各サービスのログイン情報は古閑さん自身で管理してください。

---

## 1. 全体の仕組み（どこに何があるか）

```
訪問者 → tsumugitomarimo.com
          │  ドメイン・DNS：お名前.com Navi（ネームサーバー 01〜04.dnsv.jp）
          ▼
       GitHub Pages（無料のサイト公開機能）
          │  中身：GitHub リポジトリ tsumugitomarimo/tsumugitomarimo-site の main ブランチ
          ▼
       お問い合わせフォーム → Formspree → info@tsumugitomarimo.com（Outlook の共有メールボックス）
```

| 役割 | サービス | アカウント／場所 |
|---|---|---|
| サイトのファイル置き場 | GitHub | 組織 `tsumugitomarimo` → リポジトリ `tsumugitomarimo-site`（公開・Public） |
| サイトの公開（サーバー） | GitHub Pages | リポジトリの Settings → Pages。無料・容量やアクセスの上限は実質気にしなくてよい |
| ドメイン・DNS | お名前.com Navi | ドメイン `tsumugitomarimo.com`（更新期限 2027/05/30 時点） |
| お問い合わせフォーム | Formspree（無料プラン：月50件まで） | フォーム名「HPお問い合わせ」、ID `mljjjvng` |
| 会社メール | Microsoft 365（Outlook） | info@tsumugitomarimo.com（共有）、yasuto.koga@tsumugitomarimo.com（個人） |
| 旧サイト | Studio | 2026年10月28日に切り替え済み。確認後に解約予定 |

※ GitHub の組織 `tsumugitomarimo` は、占いサイト用アカウント `felisarcana` がオーナーです（ログインは felisarcana で行う）。
※ Claude がこのリポジトリを更新できるのは、組織に「Claude GitHub App」を入れてあるため（対象はこのリポジトリのみ）。

---

## 2. ファイル構成

| ファイル | 内容 |
|---|---|
| `index.html` | トップページ。全セクション（ご挨拶／私たちの仕事 01〜03／お知らせ／会社情報／お問い合わせ）とデザイン（CSS）・動き（JavaScript）をこの1ファイルに収めている |
| `privacy-policy.html` | プライバシーポリシー（`/privacy-policy` で表示） |
| `404.html` | 存在しないURLを開いたときのページ |
| `img/` | 画像（logo, hero, sns-1〜4, pay-*, tools, street, orivimo, ogp, apple-touch-icon） |
| `favicon.png` | ブラウザのタブに出るアイコン（猫のマーク） |
| `CNAME` | GitHub Pages に独自ドメインを伝えるファイル（中身は `tsumugitomarimo.com`）。**消さないこと** |
| `.nojekyll` | GitHub の自動変換を止めるための空ファイル。**消さないこと** |
| `robots.txt` / `sitemap.xml` | 検索エンジン向けの案内 |

デザインの決まりごと（index.html の先頭 `:root` に定義）：
- 色：白地 `#FBFBF8`、文字 `#1E1F1C`、アクセントの苔色 `#3F5A3A`
- 文字：見出し「Shippori Mincho」、本文「Zen Kaku Gothic New」、数字「Cormorant Garamond」（Google Fonts）
- PC は左に縦書きの章ラベル、スマホ（幅820px以下）は横書きに切り替わる

---

## 3. HPの直し方

### Claude に頼む場合（いちばん簡単）
1. Claude の新しい会話で「GitHub の tsumugitomarimo/tsumugitomarimo-site を使って、HPの○○を直して」と頼む
2. Claude がこのファイルを読み、コードを直して main に反映 → 1〜2分で本番に出る

### 自分で直す場合（文字の修正程度）
1. https://github.com/tsumugitomarimo/tsumugitomarimo-site を開く
2. 直したいファイル（例：`index.html`）を開き、右上の鉛筆マークで編集
3. 下の「Commit changes（変更をコミット）」を押す → 1〜2分で反映

### よくある修正の場所（index.html 内で検索する語）
- お知らせを追加：`<ul class="news">` の直後に `<li>…</li>` を1つ足す（新しいものが上）
- 会社情報（住所・電話・メール）：`<dl class="info">`
- プロダクト：`<div class="products">`
- フッターの住所：`f-name`
- ページのタイトル・説明文（検索結果に出る文）：先頭の `<title>` と `<meta name="description">`

### 画像を差し替える場合
- `img/` に同じ名前で上書きアップロードすれば差し替わる
- 推奨：WebP形式、横幅は写真なら1600px程度まで

---

## 4. ドメイン・DNSの設定（お名前.com Navi）

場所：お名前.com Navi →「ドメイン」→「DNS設定／転送設定」→ tsumugitomarimo.com の「ドメインDNS」→「DNSレコード設定」

※「お名前.com レンタルサーバー」の管理画面ではありません（そちらのDNS設定は効かない）。

### 現在の正しい設定（2026年10月28日時点）

| ホスト名 | TYPE | VALUE | 用途 |
|---|---|---|---|
| tsumugitomarimo.com | A | 185.199.108.153 | HP（GitHub Pages） |
| tsumugitomarimo.com | A | 185.199.109.153 | HP（GitHub Pages） |
| tsumugitomarimo.com | A | 185.199.110.153 | HP（GitHub Pages） |
| tsumugitomarimo.com | A | 185.199.111.153 | HP（GitHub Pages） |
| www.tsumugitomarimo.com | CNAME | tsumugitomarimo.github.io | HP（www付き） |
| tsumugitomarimo.com | MX（優先0） | tsumugitomarimo-com.mail.protection.outlook.com | **メール受信。消すとメールが届かなくなる** |
| tsumugitomarimo.com（@） | TXT | MS=ms93908649 | **Microsoft 365 のドメイン確認。消さない** |
| tsumugitomarimo.com（@） | TXT | v=spf1 include:spf.protection.outlook.com -all | **メール送信の なりすまし防止。消さない** |
| autodiscover.tsumugitomarimo.com | CNAME | autodiscover.outlook.com | **Outlook の自動設定。消さない** |
| tsumugitomarimo.com | NS | 01.dnsv.jp 〜 04.dnsv.jp | お名前.com のDNS |

旧設定（Studio）：A レコード `34.111.141.225`（2026/10/28 に GitHub Pages の値へ変更済み）

**注意：DNS を触るときは、MX・TXT・autodiscover の4行は絶対に消さない。**

---

## 5. お問い合わせフォーム（Formspree）

- 送信先：`https://formspree.io/f/mljjjvng`（index.html の `<form id="contact-form" action=…>`）
- 通知先：info@tsumugitomarimo.com（Formspree の「ワークフロー」タブで変更できる）
- 通知メールに「返信」すると、問い合わせた人のアドレスに返信される
- 送信が成功するとHP上に「送信しました。2営業日以内にご返信いたします。」と表示される
- 失敗時は電話番号（080-2667-0439）への連絡を案内する文が出る
- 無料プランは月50件まで

### 届かないとき
1. Formspree の「投稿」タブを見る → あれば Formspree までは届いている
2. 「スパム」に入っていないか確認（テスト的な内容や example.com のアドレスはスパム判定されやすい）
3. Outlook の info の「迷惑メール」フォルダを確認 →「迷惑メールではない」を押す（差出人 noreply@formspree.io）

---

## 6. トラブル対応

| 症状 | 確認すること |
|---|---|
| HPが表示されない | ① GitHub の Settings → Pages に「サイトは公開されています」と出ているか ② カスタムドメイン欄が `tsumugitomarimo.com` で「DNSチェックに成功しました」か ③ お名前.com の A レコードが上の4つか ④ ドメインの更新期限が切れていないか |
| 「保護されていない通信」と出る | GitHub の Settings → Pages の「HTTPSの強制適用」にチェックが入っているか |
| 変更したのに反映されない | 1〜2分待つ → ブラウザを再読み込み。GitHub リポジトリの「Actions」で失敗（赤い×）がないか |
| 画像が出ない | ファイル名の大文字小文字・拡張子が `index.html` の記述と一致しているか |
| メールが届かない | お名前.com の MX・TXT・autodiscover が残っているか（4章の表と見比べる） |
| GitHub に Claude が書き込めない | 組織 tsumugitomarimo に Claude GitHub App が入っているか（https://github.com/apps/claude/installations/select_target） |

### 最悪の場合の復旧
- このリポジトリの中身（またはPCに保存したバックアップzip）があれば、どの無料サーバーでも同じHPを再公開できる
- GitHub の「Commits」から過去の状態に戻せる（誤って消しても履歴は残る）

---

## 7. 変更履歴

| 日付 | 内容 |
|---|---|
| 2026-10-21 | Studio のサイトをもとにコードで作り直し（改善点反映、03 自社プロダクト追加） |
| 2026-10-27 | GitHub 組織・リポジトリ作成、GitHub Pages 公開、Formspree 接続、窓口メールを info に統一 |
| 2026-10-28 | お名前.com の DNS を GitHub Pages に切り替え、tsumugitomarimo.com で公開。プロダクト欄の注記を削除 |

---

## 8. AI（Claude）向けの作業メモ

- 返答・説明は必ず日本語で（古閑さんは英語を読まない）
- このサイトはビルド不要の静的HTML。main に push すると GitHub Pages が自動で公開する
- push 前に `git pull --rebase origin main`（GitHub 側で CNAME などが追加されることがあるため）
- 変更後は https://tsumugitomarimo.com で表示確認し、スマホ幅（390px）で横にはみ出しがないかも確認する
- フォームのテスト送信は、実在しそうな文面・アドレスで行う（テスト的な内容は Formspree にスパム判定される）
- DNS（お名前.com）は古閑さんの操作が必要。触る場合はメール用4レコードを必ず残す
- 占いサイト（Felis Arcana）は会社HPに載せない方針
