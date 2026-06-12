# データ統治方針（公開用／内部用／原本アーカイブ／非表示フィールド）

公開は「誰も不当に傷つけない一次情報」であること最優先。データを4層に分けて管理する。

## 1. 公開用データ（このリポジトリ＝publishのみ）
公開してよいもの。公人・政党・企業・業界団体は公的記録に基づき実名。私人は匿名集約。
- `data/money_flow_public.csv` … 団体・企業・公人レベルの資金フロー
- `data/councilor_funds_reconciliation_public.csv` … 市議22人の関連団体・本年収入（公人）
- `data/jimin_first_branch_donors_public.csv` … 法人寄附44社（企業名・額・日付・業種。**代表者個人名・住所は除外**）
- `data/election_finance_2023_public.md` … 候補別 選挙収支（**私人献金者は「個人献金N件=計X円」に匿名集約**）
- `figures/F1〜F7` … 図版（全枚 出典フッター・規律注記入り）
- `README / LICENSE(CC BY) / DISCLAIMER / SOURCES / DATA_DICTIONARY / DATA_GOVERNANCE / uncertainty_register`

公開データリポジトリには、記事ドラフト・動画台本・制作メモを同梱しない。制作物は別の非公開制作トラックで管理し、公開データ側は根拠・データ・図版・免責に限定する。

## 2. 内部用データ（公開しない・検証/保守用）
氏名等を含む完全版。リポジトリ外（`outputs/`・`work/`）に保持し、**公開リポジトリには入れない**。
- `outputs/iwamizawa_money_flow_marahada.csv`（全フロー）、`iwamizawa_shigisen_finance_summary.md`（私人献金者の実名を含む精密版）、各stage読み取り、`iwamizawa_councilor_register.csv` など
- 用途：訂正対応・問い合わせ時の根拠確認・第2スプリントのDB構築の素

## 3. 原本アーカイブ（再ホストしない）
- 収支報告書PDF・選挙要旨PDF等は**私人氏名を含むため公開リポジトリで再ホストしない。**
- ローカル保持：`work/sorachi_reports_R7_1128/` 等（内部のみ）。
- 公開側は `SOURCES.md` で**公的機関の公表ページURL＋確認日＋Waybackスナップショット**を提示し、原本は公的機関側で誰でも確認できる形にする。

## 4. 公開不可／非表示フィールド（レッドライン）
次は公開データ・記事・図・動画に**出さない**：
- 私人（少額の個人献金者）の氏名・住所
- 企業の代表者個人名・私人の会計責任者名・私人の生年月日等
- 政治資金/選挙収支の原本PDF（私人名を含むため）
- 「同一人物と断定」する表現（同姓同名は「本人確認未了」と明記。"＝"で結ばない）
- 「癒着・不正・利権・見返り・談合」等の評価断定／政治資金と契約の因果断定
- 未確認事項を確定として書くこと（必ず🟡🔴⛔と注記）

### DB実装時（第2スプリント）の制御
- 各レコードに `publicity_level`（public / internal / restricted）を付与。
- 公開ビューは publicity_level=public のみ出力。persons テーブルの私人は role のみ（氏名非表示）。
