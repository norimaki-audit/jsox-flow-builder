# 開発メモ（DEVELOPMENT）

## 構成

- 配布物は **単一HTML**（`jsox_flow_builder.html`）。SheetJS（値のみExcel）と ExcelJS（装飾Excel）を同梱
- ソースも現状は単一HTML内にセクションコメントで区分（データモデル／フロー描画／グリッド／取込／出力／評価／AI連携／保全 等）
- 将来案：開発時のモジュール分割＋ビルドで単一HTML化（大規模リファクタは段階的に行う方針）

## データモデル（正本）

- `db` … プロジェクト全体（projectName / mode / features / processes[] / library / mappingProfiles / customCols）
- `P()` … アクティブプロセス（steps[] / rcm[] / journals[] / deficiencies[] / evidence{} / prior / revisions）
- `outProc()` …［成果物へ反映］時点のスナップショット。成果物はここから描画
- `applyAll()` … P() → 反映スナップショットへコピー
- 後方互換：読込時 `normalize()` が新フィールドを補完（既存 .json はそのまま開ける）

## 検証手順（リリース前チェックリスト）

ブラウザ（Chrome）で以下を確認：

1. クリーン起動（localStorage削除）→ スタート画面 → サンプル読込
2. 新規プロジェクト作成（J-SOX／マニュアル両用途）
3. 工程・リスク・統制の追加・編集・削除 →［成果物へ反映］→ フロー図/プレビューの同期
4. JSON保存 → 再読込（開く）→ 内容一致
5. Excel/CSV取込（サンプル.xlsx生成 → 取込 → マッピング → プレビュー → 取込 → Undo）
6. ギャップチェック／ウォークスルー／ロールフォワード表示
7. Excel出力（コンテキスト／三点セット一式）・draw.io・Mermaid・PNG/SVG・印刷プレビュー
8. 評価機能オン→評価入力→オフ→データ保持→再オンで復元
9. AI回答取込：正しいJSON／壊れたJSON（エラーメッセージ）／Undo
10. スマホ幅（≤768px）でのPC推奨案内、紹介ページの表示

簡易スモーク（構文）：メインscriptを抽出して `node --check`。

## 組み込みセルフテスト（自動）

`jsox_flow_builder.html?selftest=1` を開くと、22項目の自動スモークが実行され（件数はアプリ内定数 `SELF_TEST_COUNT` で宣言し、実数と不一致なら自動で不合格になります）、結果がダイアログと `window.__selftest` に出力されます（実データには影響せず、終了時に復元されます）。

対象: 新規作成／サンプル読込／JSON往復／後方互換（旧JSON）／CSV取込（正常・不正）／行の追加編集削除／三点セット同期／ID重複検出／ギャップチェック／ロールフォワード／Excel出力／draw.io出力／評価オンオフとデータ保持／AI取込バリデーション（正・壊れJSON）／Excel取込マッピング

## デモ・撮影用パラメータ

`jsox_flow_builder.html?pg=<page>&demo=<ai|aiimport|xls|tmpl|map>` でサンプルデータの特定画面を直接表示（スクリーンショット用・通常利用に影響なし）。

## アーカイブ

`docs/archive/` に初期デザインモック（dc.html＋support.js）・実装反映ガイド・旧スクリーンショットを保全。


## データ形式（スキーマ）とバージョン

- プロジェクトJSONは `schemaVersion`（整数）を持ちます。現行は **1**（アプリ内定数 `SCHEMA_VERSION`）。
- `schemaVersion` が無いファイルは **v0（版番号導入前の旧データ）** として扱い、移行してから読み込みます。
- 読み込みは `loadProjectData()` が唯一の入口です。**検証 → 移行 → 適用** の順で処理し、
  途中で失敗した場合は `db` と `_applied` を元に戻すため、**部分的に壊れた状態が残りません**。
  - `validateProject(o)` … 形式・必須配列・ID重複を検査（errors / warnings を返す）
  - `migrateProject(d)` … `SCHEMA_MIGRATIONS` を版番号順に適用。アプリより新しい版は読み込み前に警告
- 保存時は `schemaVersion`（読み込んだ版が新しければその値を維持）と `appVersion` を記録します。

### 形式を変更するときの手順

1. `SCHEMA_VERSION` を +1 する
2. `SCHEMA_MIGRATIONS` に新しい版番号のキーで移行関数を追加する（旧構造 → 新構造の変換のみ。項目の欠損補完は `normalize()` の役割）
3. 旧形式のサンプルJSONで読み込みを確認し、セルフテスト「スキーマ移行（旧形式→現行）」を更新する
4. 後方互換を壊す場合は CHANGELOG に移行方法を明記する

## バージョン方針

- 現行: **v0.9.0-beta**（アプリ内 `APP_VER`・README・CHANGELOG で一致させる）
- 安定化完了（CI常時グリーン＋主要導線のフィードバック反映）で **v1.0.0**
- 以降はセマンティックバージョニング（破壊的変更=メジャー／機能=マイナー／修正=パッチ）

## ソース分割の段階的移行計画（配布物は単一HTMLを維持）

### 現在のセクション境界（単一HTML内・コメントで区分済み）

`<style>`（デザイントークン/コンポーネント/印刷） → `<body>`（ナビ/各page/モーダル/オーバーレイ） → SheetJS → ExcelJS → メインスクリプト（データモデル → ユーティリティ → フロー描画 → グリッド → ギャップ → 出力(Excel/CSV/drawio/mermaid) → モード設定 → テンプレート → 取込 → 反映モデル → 成果物描画 → 評価(evalwork/oewp) → 証憑/フォルダ格納 → 棚卸 → ヘルプ → AI連携 → データ保全 → ガイド/スタート → セルフテスト → 起動）

### 主なグローバル依存

- 状態: `db` / `curPage` / `_applied` / `_viewPref` / `_tour` / `_aiCands` / `_imp` / `fscale`
- 中核関数: `P()` `outProc()` `applyAll()` `normalize()` `show()` `esc()` `toast()`
- DOM ID結合が強い層: グリッド描画（stepBody等）・モーダル群

### 分割候補（リスク低い順）

1. 定数（STEP_TYPES / PHASE_COLORS / ASRT_* / SAMPLE_GUIDE / HELP_CAT_META）
2. サンプルデータ・テンプレート（exampleDB / TEMPLATES）
3. ユーティリティ（esc / download / dataUrlToBlob / idNum / rcmSorted / toast）
4. セルフテスト（runSelfTest — 純粋に付加的で最初の切り出しに最適）
5. ヘルプ記事データ（HELP配列）
6. AI連携（プロンプト生成・取込パース）
7. 出力層（drawio/mermaid/ExcelJS変換）
8. 最後: データモデル・描画中核（十分なテスト整備後）

### ビルド設計（案）

```
src/
  00_style.css  10_body.html  20_vendor/(sheetjs,exceljs)
  30_model.js ... 90_boot.js  tests/selftest.js
build.js   # マーカー置換で dist/jsox_flow_builder.html に連結
dist/jsox_flow_builder.html   # 従来どおり単体配布
```

- `build.js` は Node 標準のみで実装（依存ゼロ）。CI で「ビルド結果 = リポジトリのHTML」を検証し乖離を防ぐ
- 移行単位ごとに: 切り出し → ビルド → セルフテスト22項目 → コミット、の小さなサイクルで進める
- 一度に全面リファクタリングしない。各段階で既存JSON・自動保存の互換を維持

## Release用配布HTMLの作成手順

リポジトリ構成は変えず、Release作成時にローカルでコピーして添付する運用とします（開発元と配布物の乖離防止のため、必ずタグを打ったコミットからコピーする）。

```bash
git checkout v0.9.0-beta
cp jsox_flow_builder.html jsox_flow_builder-v0.9.0-beta.html
gh release upload v0.9.0-beta jsox_flow_builder-v0.9.0-beta.html assets/samples/sample_project.json
```

- 配布ファイル名はタグと一致させる（`jsox_flow_builder-vX.Y.Z(-beta).html`）
- 添付は「単体で使い始められる」最小セット: 配布HTML＋サンプルJSON（必要に応じてサンプルExcel）
- アップロード後、ダウンロードして `?selftest=1` が18/18で通ることを確認する
