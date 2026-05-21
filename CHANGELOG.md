# CHANGELOG — Asia Honpo Corporate Website

**Tier:** T1 Public
**Level:** L2 Official Knowledge
**Repo:** `asia-honpo/website-public`

このリポジトリのバージョン履歴。コーポレートサイト本体(7 pages, clean URLs, Cloudflare Workers hosted)の改訂を記録。

形式: [Keep a Changelog](https://keepachangelog.com/) を簡略化したもの。

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
