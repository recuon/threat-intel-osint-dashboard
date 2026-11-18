# Supplier Incident Atlas — 巻き込み規模ランキング 2026

公開用の静的ページ。事故は共通サプライヤー単位で1件とし、取引先の個別公表や続報は二重計上しない。

- [公開ページ](https://recuon.github.io/threat-intel-osint-dashboard/supplier-incident-atlas/)
- [データの編集](https://github.com/recuon/threat-intel-osint-dashboard/edit/main/supplier-incident-atlas/data.csv)
- [原稿HTML](index.html)
- [データCSV](data.csv)

## 更新方法

**data.csv を編集してコミットするだけ**で、公開ページのランキング・検索・CSVエクスポートに反映される。ビルドやJavaScriptの変更は不要。公開ページはファイルをネットワークから読み込み、ローカルファイルでCSV取得ができないときは初版データを表示する。

CSVの1行は **1事故**。必須列は id（変更しない事故ID）, name, group, count, source。グループは org（企業）, facility（店舗・施設）, contract（契約）, pending（総数未確定）。count が未確定の場合は空欄。confirmed / possible / mixed で判定を分ける。

新規行には公式発表への source と、その日付 source_date を必ず記載する。企業数・店舗数・契約数を混同しない。取引先の個別通知や同一事故の続報は新規行にせず、既存事故の記述と根拠だけ更新する。同じサプライヤーでも独立した侵害であることが一次情報から確実に区別できる場合は別事故IDを付与する。

## 公開状態と注意

初版の基準日は 2026-11-18。公開情報に基づく暫定順位であり、全数網羅、全企業への影響確定、損害や過失の評価を意味しない。初版のHTML内に内蔵されたデータはオフライン表示用のフォールバックであり、ウェブ表示時は data.csv が優先される。

このサブページは既存の OSINT & Threat Intelligence Toolkit のルートページから独立しており、ルート側のファイルを改変しない。
