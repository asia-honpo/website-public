# Asia Honpo Corporate Website

株式会社アジア本舗 (Asia Honpo Co., Ltd.) のコーポレートサイト。

**Live**: https://www.asiahonpo.co.jp/
**Tier**: T1 Public

---

## 🏗️ Tech Stack

- **静的HTML** (7ページ、合計約210KB)
- **Inline CSS** (外部CSSファイルなし、超軽量)
- **Google Fonts**: Noto Serif JP / Noto Sans JP / Cormorant Garamond / JetBrains Mono
- **画像依存ゼロ** (グラフィックは全てinline SVG / Unicode)
- **JavaScript依存ゼロ**
- **ホスティング**: Cloudflare Pages (GitHub auto-deploy)

---

## 📄 Pages

| URL | ファイル | 内容 |
|---|---|---|
| `/` | `index.html` | Home — ホーム |
| `/business` | `business.html` | 事業について |
| `/company` | `company.html` | 会社概要 |
| `/journal` | `journal.html` | 越境ECで、10年やってきて。 |
| `/contact` | `contact.html` | お問い合わせ |
| `/tokutei` | `tokutei.html` | 特定商取引法に基づく表記 |
| `/privacy` | `privacy.html` | プライバシーポリシー |

→ Cloudflare Pages のクリーンURL機能により、`/business` で `business.html` が自動配信されます。

---

## 🚀 Deployment

`main` ブランチへの push で Cloudflare Pages が自動デプロイ。

```bash
# ローカルで変更
vim index.html

# プッシュで自動デプロイ
git add -A
git commit -m "Update home hero copy"
git push origin main
```

---

## 🎯 設計原則

- **対象読者**: 真摯にものづくりに向き合う製造業経営者 (60〜75歳)
- **目的**: SEO集客ではなく、「裏取り(due diligence)」のための信頼の検証装置
- **トーン**: 自慢しない、ただ淡々と事実を積む

---

## 📋 KODAWARI 設計境界

サイトに掲載しない情報:
- フランチャイズプログラムの詳細
- 工場名 (取引先各社の同意取得まで非開示)
- 内部組織用語・スキーム理論

---

## 📞 Contact

- **Email**: info@asiahonpo.co.jp
- **所在地**: 〒171-0031 東京都豊島区目白2-3-15 ソフィア目白 1003号

---

© 2015-2026 ASIA HONPO CO., LTD. All rights reserved.
