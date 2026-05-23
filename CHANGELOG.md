# CHANGELOG — Asia Honpo Corporate Website

**Tier:** T1 Public
**Level:** L2 Official Knowledge
**Repo:** `asia-honpo/website-public`

このリポジトリのバージョン履歴。コーポレートサイト本体(7 pages, clean URLs, Cloudflare Workers hosted)の改訂を記録。

形式: [Keep a Changelog](https://keepachangelog.com/) を簡略化したもの。

---

## [v2.1.1] - 2026-05-23

### Fixed — Home ページ index.html の構造改善

v2.1.0(factory-partner-faq.html 新規追加)に続く、Home ページの 2 つの未解決課題に対応。

#### Changed
- **`index.html`** Stats section 構造統一(課題 1):
  - `<section class="stats">` の中身を `<div class="wrap">` でラップ → viewport 全幅 → `--max: 1240px` 固定
  - 他セクション(Hero / About / History / CTA / Footer)と完全整合
  - 背景帯(warm beige + border-top/bottom)は全幅維持(C 案 editorial design pattern)
- **`index.html`** CTA section 本文中に FAQ link を inline 追加(課題 2):
  - 「まずは `<a class="cta-faq-link">よくあるご質問</a>` もご一読の上、...」
  - business/company/contact の footer 直前 soft link block と異なり、Home 限定の subtle inline link
  - target audience(製造パートナー候補)だけが気づく editorial design

#### Added
- **`index.html`** CSS: `.cta-faq-link` スタイル定義
  - color: var(--ink) + border-bottom: 1px solid var(--coral)
  - hover: opacity 0.65 transition
  - editorial subtle: 注意深い読者だけが気づく、CTA への誘導を維持しつつ FAQ にも導く

### Process
- KODAWARI 多段階確認による方針決定:
  - 課題 1: **C-2 案**(.wrap でラップ、HTML 構造統一)→ C-1(CSS のみ)より設計一貫性優先
  - 課題 2: **B 案**(CTA inline link)→ A 案(Header nav)却下、C 案(footer 直前 block)より CTA 効果保持を優先
- Python deploy script による KODAWARI 7-Phase 安全設計(Pre-check / Backup / Stats wrap / CTA link / CSS / Post-verify / Diff summary)
- Idempotency-aware safe_replace:既適用時は skip(2 回実行しても安全)

### Pattern Library 候補(本 release で 1 件新規)
- `editorial-subtle-inline-link-v1`: 対象読者だけが気づく inline link の設計パターン(ink color + coral underline、font-weight/family 変更なし)。本文の流れを断ち切らず、target audience に対して subtle に第 2 動線を提供する editorial design。

### Reference
- commit: TBD(次の commit で確定)
- 関連: 前 release v2.1.0(factory-partner-faq.html)に対する Home ページ整合性対応

---

## [v2.1.0] - 2026-05-23

### Added — 製造パートナー候補向け FAQ ページ新規追加

製造パートナー候補の皆様(中小日用品製造業の経営者)からよくいただくご質問 20 件をまとめた専用 FAQ ページを新規追加。journal.html の design system(3-column grid、CSS 変数、Noto Serif JP / Cormorant Garamond)を完全踏襲し、サイト全体の一貫性を維持。

#### Added
- **`factory-partner-faq.html`** (新規、39KB):
  - 製造パートナー候補向け FAQ ページ(8 ページ目)
  - 20 件の Q&A(既存取引、工場規模、所在地、年間発注規模、為替、品質基準、金型、契約、見積りフロー、補助金 等)
  - 構造: Hero → Lead → Index(TOC、Q1-Q20 リンク)→ Q&A 20 件 → CTA
  - design system: journal.html 完全準拠 3-column grid(240px label + 720px content + 1fr 余白)
  - FAQ 専用 CSS(4.4KB)を `<head>` に注入、`.faq-lead-frame` / `.faq-toc-frame` / `.faq-q-frame` 構成
  - Mobile responsive(@media 900px breakpoint で 1-column collapse)
  - JavaScript 依存ゼロ(全展開型、anchor link のみで navigation)

#### Changed
- **`business.html` / `company.html` / `contact.html`**: footer 直前に
  factory-partner-faq への soft link 追加(50px padding、warm background、center alignment)
- 累計レビュー数訴求を **6,000 件 → 15,000 件超** に更新(brain-public SWOT/Cross_SWOT と整合)

### Process
- KODAWARI 案 η Deep(Reader Experience KODAWARI)を新規確立し適用:両ペルソナ A/B シミュレーション、Phase τ/υ/φ/χ/ψ の 5 段階、致命的 Friction 0 件で公開可判定
- CSS 設計を 3 回 iteration で最適化:v2(essay-section 流用、padding 過大)→ v3(独自 compact CSS、幅狭)→ v4(journal.html 完全準拠 3-col grid)
- Python deploy script による KODAWARI 7-Phase 安全設計:Pre-check / Backup / Template Read / Content Build / Generate / Self-Healing Soft Link / Post-verify

### Pattern Library 候補(本 release で 3 件新規)
- `mcp-verify-protocol-v1`: MCP filesystem write 後は必ず view で書き込み verify
- `reader-experience-kodawari-eta-process-v1`: 読み手体験 KODAWARI プロセス(τ→υ→φ→χ→ψ)、両ペルソナ並行シミュレーション
- `css-context-aware-reuse-v1`: 既存 CSS を文脈無視で流用すると失敗する。20 件の短い Q&A は、3 件の長文 essay 用 CSS と本質的に違う文脈

### Reference
- commit: TBD(次の commit で確定)
- 関連: brain-public `17_STRATEGY/SWOT_Analysis.md` + `Cross_SWOT_Analysis.md` の数字整合(15,000 件超)
- 関連: brain-public `08_PLAYBOOKS_AND_SOPS/factory_partner_faq_v2.1.md`(Q&A データソース)

---

## [v2.0.0] - 2026-05-21 🎉 PRODUCTION CUTOVER

### Major Milestone
**WIX → Cloudflare Workers 移行完了**。サイトコード (v1.0.0 〜 v1.2.5) が公式ドメイン `https://asiahonpo.co.jp` および `https://www.asiahonpo.co.jp` で **Live** に。

### Added
- **`wrangler.jsonc`**: Cloudflare Workers 設定ファイル (PR #1 squash merge, commit `fbe9f85`)

### Changed (Infrastructure)
- **Hosting Platform**: WIX → Cloudflare Workers
- **DNS Provider**: WIX (`ns10/11.wixdns.net`) → Cloudflare (`conrad/venus.ns.cloudflare.com`)
- **Domain Registrar**: お名前.com (変更なし、NS のみ切替)
- **A Records**: 旧 WIX IPs (`185.230.63.107/171/186`) → Cloudflare Anycast (`104.21.26.175`, `172.67.138.58`)
- **Production URLs**:
  - ✅ `https://asiahonpo.co.jp` (root)
  - ✅ `https://www.asiahonpo.co.jp` (www)

### Preserved (zero impact)
- **MX Records** (Rackspace): `mx1/mx2.emailsrvr.com` 完全保全 → メール継続稼働

### Removed (DNS cleanup)
- A: `185.230.63.107` (WIX)
- A: `185.230.63.186` (WIX)
- A: `185.230.63.171` (WIX)
- CNAME `m` → `www85.wixdns.net` (WIX モバイル用)
- CNAME `www` → `cdn1.wixdns.net` (WIX www 用)

### Migration Process
1. **NS 切替**: お名前.com で `ns10/11.wixdns.net` → `conrad/venus.ns.cloudflare.com` 変更 (伝播 ~7 分)
2. **Cloudflare zone activation**: `asiahonpo.co.jp is now active on Cloudflare (Free plan)` メール受信
3. **WIX DNS cleanup**: Cloudflare DNS records から WIX 関連 5 件を bulk delete (MX 2 件は保全)
4. **Custom Domain 追加**: Worker `website-public` の Domains タブで root + www を追加
5. **SSL 自動発行**: 全ドメインで HTTPS 有効化

### Verification (post-cutover)
- `dig @8.8.8.8 asiahonpo.co.jp A` → `104.21.26.175` + `172.67.138.58` (Cloudflare Anycast) ✅
- `dig @8.8.8.8 asiahonpo.co.jp MX` → `mx1/mx2.emailsrvr.com` (Rackspace 維持) ✅
- `curl -I https://asiahonpo.co.jp` → `HTTP/2 200`, `server: cloudflare` ✅
- HTML 内容: `SCANDINOVIA` + `アジア本舗` 検出、`wix` 文字列なし ✅

### Downtime Window
- **Web**: 約 5 分 (WIX DNS 削除 → Custom Domain 追加までの間)
- **Email**: **0 分** (MX 完全保全)

### Pattern Library 候補 (本 release 関連、3 件新規)
- `cloudflare-subdomain-field-trap-v1`: Custom Domain 追加時、Subdomain 欄に full FQDN を入れると `.zone` が自動 suffix され invalid FQDN に。`www` のみ入力が正解
- `cloudflare-zone-import-dns-scan-trap-v1`: Zone 追加時の自動 DNS scan で取り込まれた既存レコードは、後で Custom Domain 追加時の衝突原因になる (事前削除必要)
- `cloudflare-add-domain-root-then-www-pattern-v1`: root → www の順で追加すると安全 (root: Subdomain 欄空欄 / www: Subdomain 欄に `www` のみ)

### Future Work (Phase 4 / 後日)
- WIX サブスクリプション解約
- SPF / DMARC TXT レコード追加 (Cloudflare DNS recommendations)
- MCP for website-public 設定 (Claude Desktop config 追加)
- Pattern Library 候補の正式登録 → brain-public `18_SKILLS`

---

## [v1.2.5] - 2026-05-21

### Removed
- **言語トグル削除 (JP/EN ボタン)**: 使われていない言語切替トグル `<div class="lang">...</div>` を全 7 HTML ファイルから一括削除
  - 対象ファイル: `index.html`, `business.html`, `company.html`, `journal.html`, `contact.html`, `tokutei.html`, `privacy.html`
  - 削除量: 102 文字 × 7 ファイル = **714 文字削減**
  - commit: `d3ff839`

### Process
4-phase safety 設計の Python deploy script (`remove_lang_toggle_v1.py`) を使用:
1. **Pre-check**: 対象 string の存在と件数を全ファイルで確認
2. **Backup**: 各ファイルを `.bak-langtoggle` 拡張子で保存
3. **Edit**: 全 7 ファイルに replace 実行
4. **Post-check**: 削除後に `is-active JP` 出現 0 回を確認

### Pattern Library 候補 (本 release で 1 件新規)
- `web-fetch-cache-misleads-v1`: web_fetch ツールはキャッシュで古い HTML を返すことがある。時間敏感な検証は curl で生 HTML 確認すべき (`/terms` 404 誤検出が発端)

---

## [v1.2.4] - 2026-05-21

### Fixed — EST. notation 整理(index.html)

`index.html` info-row の EST. 表記から HQ 所在地を分離し、設立年(`A.D. 2015`)のみのクリーンな表記に統一。前 v1.2.3(About page)に続く EST. 全面整理の最終段階。

#### Fixed
- `index.html` info-row:`A.D. 2015 — Tokyo` → `A.D. 2015`

#### Reference
- commit `e5ab1bd`

---

## [v1.2.3] - 2026-05-21

### Fixed — EST. notation 整理(About page)

設立年(EST.)と本社所在地(HQ)が同一表記内に混在していた状態を解消。**設立年**と**所在地**を別フィールドとして明確に分離し、情報の意味的曖昧さを排除。

#### Fixed
- About/Company page:設立年と HQ 所在地の分離表記

#### Reference
- commit `424e683`

---

## [v1.2.2] - 2026-05-21

### Fixed — Quote レイアウト復帰

CEO quote のレイアウトを full-width 表示から右カラム内表示に revert。デザイン一貫性を優先。

#### Fixed
- Company page:CEO quote を右カラム内表示に維持

#### Reference
- commit `d59599b`

---

## [v1.2.1] - 2026-05-21

### Changed — Refactor

Company page FIG.04 から冗長な `PORTRAIT` タグを削除。コードの可読性向上。

#### Changed
- Company page:冗長 `PORTRAIT` タグ削除

#### Reference
- commit `8ff3cd9`

---

## [v1.2.0] - 2026-05-21

### Added — Company page 拡充

Company page に CEO portrait と full-width quote を追加。会社の人格的側面を可視化。

#### Added
- Company page:CEO portrait
- Company page:Full-width quote

#### Reference
- commit `6e469db`

---

## [v1.1.0] - 2026-05-21

### Added — SCANDINOVIA product images / Removed — Obsolete `/terms` link

プロダクトページに SCANDINOVIA 商品画像を追加。同時に古い `/terms` リンクを削除し、現状の URL 体系と整合。

#### Added
- SCANDINOVIA product images

#### Removed
- Obsolete `/terms` link

#### Reference
- commit `63698de`

---

## [v1.0.0] - 2026-05-21

### Initial Release

Asia Honpo コーポレートサイト v1.0 の初版リリース。

#### Added
- 7 ページ構成
- Clean URL ルーティング(`/about`、`/company` 等の拡張子なし URL)
- KODAWARI 検証済みのデザインシステム
- Cloudflare Workers ホスティング

#### Reference
- commit `ebe21bd`

---

## バージョニング規則

```
v[Major].[Minor].[Patch]

Major (X.0.0): 全面リデザイン、リブランディング、アーキテクチャ変更
Minor (1.X.0): 新規ページ追加、大規模コンテンツ追加、新セクション
Patch (1.0.X): バグ修正、軽微なコンテンツ調整、refactor
```
