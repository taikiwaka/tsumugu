# データ辞書と計測

## 公開デモのJSON
version=1。profile：家族の語りnote、模擬下書きdraft（likes/care/will/next/at）、承認approved。
logs[]：id、at(ISO日時)、facility(A/B/C)、staff(架空ID)、note、result、response、base/ minutes（業務時間・分）、share。
feedback[]：id、at、logId、before/after（1–5）、comment。家族の回答は支援記録ごとに1回。
money[]：id、at、purpose、amount（円）、checked、checkedAt。
facilities[]：id/name/status/fee。feeは仮説価格。statusは手動入力した模擬契約段階。
audit[]：time/action。端末内操作記録。改ざん防止なし。
handoff：模擬引き継ぎのチェック。

## デモ計算式
- 時間差：全支援記録の (base-minutes) の算術平均。負値を含む。0件は「—」。実験の中央値・対応サンプル比較とは別。
- 安心度変化：紐付け可能な家族回答の (after-before) 平均。0件は「—」。未回答は0点で補完しない。
- 入金施設：statusが「入金確認」の施設数。実証済み売上ではない。
- 支出累計：money.amountの合計。デモ全期間。1万円超過は要確認表示。不正検知ではない。

## 本実験で追加するテーブル
participants（仮名ID・施設・対象期間・担当者・本人への説明/権限確認の参照）、staff_cohort（計測対象分母・勤務条件・除外理由）、profile_versions（原文・根拠・確認者）、support_opportunities（実施前の機会・予定・選択肢・拒否/不明・結果）、family_surveys（家族仮名ID・測定時点・欠測理由）、time_studies（担当者・類似業務種・導入前後・追加負担）、contracts/invoices（初回/更新・税別価格・契約日・入金日・証跡参照）、support_cost（初期/定常・実工数・単価）、incidents、audit_events。

時刻の保存はUTC、表示と週の区切りはAsia/Tokyo。実験週は施設ごとの導入日を起点とし、同じカレンダー週で混同しない。実験の継続率は事前固定した対象支援者の分母を使う。操作ログだけで利用継続を算出しない。

個人単位の変化と施設別のばらつき・欠測・離脱を集計し、3施設の総平均だけで判断しない。観測数は本人・家族・支援者・出来事を区別し、同一人物の複数出来事を独立人数とみなさない。
