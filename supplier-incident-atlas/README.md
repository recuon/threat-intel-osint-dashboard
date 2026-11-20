# Supplier Incident Atlas — 2026 巻き込み規模比較

公開ページ: https://recuon.github.io/threat-intel-osint-dashboard/supplier-incident-atlas/

## 表示する3指標

1. **公式公表値** — `count`, `unit`: 公表された企業・店舗・施設・契約・システム数を元の単位のまま掲載。数の単位は比較・加算しない。
2. **推定事業者数** — `est_low`, `est_high`, `est_kind`, `est_basis`: 店舗・契約・システムから独立事業者数への仮換算。**実測値や統計的な信頼区間ではない**。母数の一次情報が不確かなものは「条件付き試算」。
3. **最大潜在母数** — `potential_count`, `potential_unit`, `potential_basis`: 影響し得た対象の母数。過去利用者、契約レコード、試験データ等を含み得るため、独立した被害法人数とは限らない。

`confirmed_org_count` は一次情報で独立した組織数を確認できた場合だけ入力する。未確認なら空欄（0ではない）。

## ブラストメールの二層構造

配信基盤の契約者情報以外にも影響があった421契約と、販売管理上の33,382契約関連レコードは同じ事故の異なる影響範囲で、重複するため合算不可。配信先情報については対象が不確定で、240〜345事業者という数字は仮定に基づく試算。販売管理情報の約11,000〜30,000事業者も、レコードの組織対応率50〜90%・1組織あたり1〜1.5レコードという実測根拠のない条件付き試算で、ランキングと合算しない。

## データ更新

[CSVをGitHub上で編集](https://github.com/recuon/threat-intel-osint-dashboard/edit/main/supplier-incident-atlas/data.csv) → `main` にコミットする。公開ページがCSVを取得し、自動的にリストを再描画する。ブラウザでCSVを取得できない場合はHTML内蔵の初版データを表示する。ローカル/offline版の内蔵データは別途更新すること。

CSVは1事故1行。同じサプライヤーでも一次資料で独立した別事故と確認できた場合にのみ事故IDを分ける。顧客企業からの個別報告や、同一事故の続報は既存行を更新する。公表値が増えた場合は `count` だけでなく `source`, `source_date`, `est_basis`, `potential_basis` も更新する。

CSVの空欄は**未確認**の意味。推定区間が確定値であるように見える表記に変更しないこと。`source_label` は原資料の説明に用いる。更新期間外の事故を追加する際は掲載範囲も明記する。

## 制約

初版の基準日: 2026-11-18。直近の横断調査: 2026-11-20（掲載20事故）。掲載は網羅的全件ではない。シナリオの前提は公開資料をもとにした仮定であり、メーカー公式の流出法人数を示すものではない。過失や損害の程度の格付けではない。

## 2026-11-19 日次レビュー（第一回）

- 追加7事故：LAFOOL（182社確認）、SCALA-IASK（4社確認、初報最大5社を訂正）、SMBC-CF（複数提携金融機関・総数未確定）、SONIC-COMSBI-ENT（LINE認証情報の読み出し確認／個人データ流出は未確定）、SONIC-COMSBI-SAAS（別基盤・別侵害、複数団体の情報持ち出し確認）、CONNECTWISE-SKYKICK（不正サインイン162 M365テナント観測。ただし法人・流出情報数ではない）、QUBOLE（複数顧客のAWS IAMロール不正利用）。
- 既存レコード更新1件：PLAIDを11/18 21時の公式進捗に更新。流出企業総数・サービス復旧目途は未公表。
- **見送り**：チャットプラス 11/17公開の不正アクセス（https://chatplus.jp/news/news20261117/）。3サービス共用Webサーバで顧客の個人データ閲覧・取得の可能性を発表したが、実際に複数の独立企業へ波及したか一次情報で判定できず、本順位への新規計上は保留。次回以降再確認。
- 既存9件の一次資料と続報を照合。既存推定レンジの確定的な再計算を裏付ける新資料は確認できなかったため維持。過去の推定は公式確定値と混同しない。
- 同じベンダーのソニックムーブ2案件は提供基盤と侵害日時の異なる独立事故。SMBC-CF提携先銀行やラフール再販元の個別報告は別事故として追加しない。

一次資料は各事故の `source` フィールドを参照。海外調査機関が原観測の報告者となるケースは、その出典と公式ベンダー公表の区別を詳細欄で示す。

## 2026-11-20 日次レビュー（第二回）

- **新規4事故**：OPENLOGI（共通出荷代行から多数の荷主へ波及、発表総法人は未確定）、TERILOGY-CLOUDTRIAGE（6社で不審セッションを確認、流出未確認）、SECURITIZE-JP（11/2時点で発行体3社分の個人情報持ち出しを確認、金融機関などの総数未確認）、KLUE-OAUTH（6月侵害の見落とし補完、Huntress/HackerOne/OneTrustの3社が一次公表、総数未確認）。発行体3社およびKlueの3社は**確認下限**で、全影響先数ではない。
- **既存続報2事故**：PLAIDは11/19 11時の提供元進捗と三菱UFJ銀行11/18（約650万件）、タイミー11/19（求人事業者担当者最大226,662名分）の一次公表を追加。両社の人数・レコード数は事業者数へ換算しない。CONNECTWISE-SKYKICKは11/19 19:20 UTCの全機能復旧告知に更新。テナントごとの再認可・バックアップ成功確認がまだ必要。
- **訂正0、推定数値変更0**。公式確認対象6社は不審アクセスの対象であり、データ流出の確認6社ではない。オープンロジについてpiyologが11/19時点に収集した「99件の関連公表」は、公表主体・再委託・ブランド等の重複可能性があるため、**99社として掲載していない**。https://piyolog.hatenadiary.jp/entry/2026/11/19/183634
- 注目すべき公表の一次資料：オープンロジ第2報 https://corp.openlogi.com/news/notice/notice-20261117/ 、鹿島アントラーズ https://www.antlers.co.jp/blogs/news/261118ytxj2u 、Brave group https://bravegroup.co.jp/news/12429/ 、テリロジーHD https://www.terilogy-hd.com/news/8168.html 、NTTデータ https://www.nttdata.com/global/ja/news/release/2026/110200/ 、Huntress https://www.huntress.com/blog/klue-breach-investigation 、HackerOne https://www.hackerone.com/security-updates/klue-2026-06 、OneTrust https://www.onetrust.com/blog/update-from-onetrust-on-klue-salesforce-security-incident/ 。
- 11/17のChatPlus不正アクセスは引き続き、複数の独立顧客企業のデータ影響を一次情報だけでは確認できず、追加を保留。https://www.chatplus.jp/news/news20261117/
