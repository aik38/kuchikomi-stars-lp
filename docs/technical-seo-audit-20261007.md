# 技術SEO最終監査（2026-10-07）

完成済みLPの本文・見出し・料金・FAQ本文・CTA文言/リンク/配置・デザイン・配色・画像・ロゴ・フォント・余白・レイアウト・セクション順・アニメーションを維持し、不可視の技術項目のみを更新。

- 対象: `aik38/kuchikomi-stars-lp`
- 本番: https://kuchikomi-stars.com/
- 作業前main: `ff3b3266c7a91c61b2211cf70f00226f75687a1e`
- 作業branch: `work/kuchikomi-stars-technical-seo-20261007`
- 作業前Pages: 同mainの `pages build and deployment` 成功、run `37296872675`
- 作業前本番HTML: mainの `index.html` とバイト一致、200応答

## 監査と実施内容

| 項目 | 状態・対応 |
| --- | --- |
| title / description | 全7公開ページに存在し、既存本文と対応。文言を維持 |
| canonical | 全7ページのHTTPS・non-www・末尾スラッシュURLを維持。各ページ1個 |
| index | 公開7ページをindex/followと明示し、大きい画像プレビューを許可。404の既存noindexを維持 |
| robots.txt | 全クローラの取得を許可し、正しいsitemapを指定。既存ファイルを維持 |
| sitemap.xml | 正規URL7件を維持。古いlastmodを、各HTMLの実際の直近ソースcommit日 `2026-09-30` に整合。技術監査日への一律更新はしていない |
| 構造化データ | 各ページ1個のJSON-LDを追加。サービス/FAQ内容は現行LPから転記 |
| OGP | 既存title/description/imageを維持。欠けていたlocale/site name、画像形式・寸法・説明等を補完 |
| Twitter Card | 未実装ページを補完し、各ページの既存OGP情報と同じtitle/description/imageを設定 |
| favicon / manifest | 既存SVG faviconは正常。PWA機能を持たない静的サイトのためmanifestは追加しない |
| GA4 | 全公開ページの `G-1ZKN01T0YL` と既存イベント実装を維持。タグ追加・管理画面操作なし |
| HTML | 各ページの日本語lang、viewport、1個のh1/mainを確認。head以外では属性間の空白、名前付きdivのgroup role、不正なiframe幅属性だけを整理 |
| 画像 / フォント | 本文画像はHTML/CSSで構成。未参照WebPを含め、画像・SVG・CSS・JSの全資産はバイト一致。外部フォント通信なし。新規preload/preconnectは不要 |
| 404 | 存在しないURLは404。深いURLでもCSS/faviconを取得できるよう、404.htmlの資産参照をルート相対に修正。404の文言・CSS・本文は維持 |
| URL別名 | `/index.html` は200でHTTPS `/` にcanonical。ディレクトリのスラッシュなしは301でスラッシュありへ。HTTPS wwwは301でnon-wwwへ |
| HTTP | 現状はHTTP non-wwwも200、HTTP wwwはHTTP non-wwwへ301、GitHubの公開用別名はHTTP non-wwwへ301。取得されるHTMLのcanonicalはHTTPS。HTTP転送・配信基盤の設定変更は行っていない |
| 公開デモ | `/demo/` はサービスの4ステップを示す公開説明ページで、管理/検証専用ページではない。index・sitemap掲載・CTAリンクを維持 |
| AI検索向け情報 | 通常HTMLで本文を取得可能。Organization/WebSite/ServiceとFAQ/パンくずの関係をJSON-LDで明示。追加本文・隠しキーワード・llms.txtなし |

## 構造化データ

- トップ: Organization（既存ブランド名・URL・公開メール）、WebSite、WebPage、Service 3件、FAQPage。
- Service: Googleクチコミ10件保証、クチコミ集客プラン、MEO・AIO運用プラン。サービス名と説明は既存LPに存在するもののみ。
- FAQPage: 表示済みFAQ9件の質問/回答を完全一致で転記。
- サブページ: WebPage（問い合わせはContactPage）と、表示済みのパンくずに対応するBreadcrumbList。
- 架空の評価・レビュー・人物・住所・実績を追加していない。Offerや価格を追加していない。
- FAQPageはSchema.orgの機械可読性を目的とする。検索での特別な表示や順位上昇を保証しない。

## 検証結果

1. 本文全テキスト、見出し全テキスト、全リンク先、GA4 ID、CSS/JS/全画像資産の変更前後一致。
2. Chromiumで8ページ（公開7ページと404.html）×5幅（1440 / 768 / 390 / 375 / 320px）を比較。40組すべてのスクリーンショットがピクセル一致、DOMテキスト・要素の位置/寸法/スタイルも一致。横スクロールの発生なし。
3. スマホメニュー開閉・Escapeキー・FAQ開閉を確認。動作後の表示も一致。
4. 153件のサイト内リンク/アンカー/参照資産に欠損なし。GA4等の外部リクエストと問い合わせiframeは、比較時のみ同じ空応答に置き換え、外部表示の変動とテスト計測を除外。iframeのURL・CSS・配置は維持。
5. HTML検証の構文・属性・ARIAエラー0件。既存の末尾空白lintと「ARIA表よりnative tableを推奨する」スタイル規則は検証対象から除外。表示維持のため、既存ARIA tableを全面改造していない。
6. JSON構文、重複head項目、FAQ本文一致、Schema.org公式語彙の型/プロパティ/継承domainIncludesを検証。49個の型付きノードが適合。
7. robots/sitemapの整合性、正規URL7件・重複なし、404のnoindexを確認。
8. `git diff --check` 合格。

## 性能・Core Web Vitals

同一Chromium・本番相当の静的ローカル配信でLighthouseを変更前後比較。GA4の外部通信を同条件で除外。以下はラボ値であり、実利用者の計測値ではない。

| 指標 | スマホ変更前 | スマホ変更後 | PC変更前 | PC変更後 |
| --- | ---: | ---: | ---: | ---: |
| Performance | 99 | 99 | 100 | 100 |
| SEO | 100 | 100 | 100 | 100 |
| Best Practices | 100 | 100 | 100 | 100 |
| LCP | 1.835秒 | 1.837秒 | 0.515秒 | 0.511秒 |
| CLS | 0 | 0 | 0 | 0 |
| TBT | 0ms | 0ms | 0ms | 0ms |

重大な性能問題は確認されず、CSS/JS/読み込み挙動を維持。数msの変動を改善効果として扱わない。未使用CSS/圧縮/キャッシュに関するLighthouseの最適化候補は、表示維持と配信設定への不介入を優先して実装していない。TBTはINPではなく、実利用者のINP・CWV合否は今回判定していない。

## 操作範囲

Google Analytics / Search Console / Ads管理画面、Cloudflare、DNS、メール設定、`review.kuchikomi-stars.com` のシステム、料金・サービス仕様には変更を加えていない。

## 参照した公式仕様

- https://schema.org/Organization
- https://schema.org/Service
- https://schema.org/FAQPage
- https://schema.org/WebPage
- https://schema.org/version/latest/schemaorg-current-https.jsonld
- https://developers.google.com/search/docs/crawling-indexing/sitemaps/build-sitemap
- https://developers.google.com/search/docs/appearance/ai-features

公開後のcommit・Pages workflow成功・本番ファイル一致の確定結果は、最終報告とGitHub履歴で確認する。
