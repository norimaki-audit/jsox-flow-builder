# 開発メモ（DEVELOPMENT）

## 構成

- 配布物は **単一HTML**（`jsox_flow_builder.html`）。SheetJS（値のみExcel）と ExcelJS（装飾Excel）を同梱
- ソースも現状は単一HTML内にセクションコメントで区分（データモデル／フロー描画／グリッド／取込／出力／評価／AI連携／保全 等）
- 将来案：開発時のモジュール分割＋ビルドで単一HTML化（大規模リファクタは段階的に行う方針）

## データモデル（正本）

- `db` … プロジェクト全体（projectName / mode / features / processes[] / library / mappingProfiles / customCols）
- `P()` … アクティブプロセス（steps[] / rcm[] / journals[] / deficiencies[] / evidence{} / prior / revisions）
- `outProc()` …［反映］時点のスナップショット。成果物はここから描画
- `applyAll()` … P() → 反映スナップショットへコピー
- 後方互換：読込時 `normalize()` が新フィールドを補完（既存 .json はそのまま開ける）

## 検証手順（リリース前チェックリスト）

ブラウザ（Chrome）で以下を確認：

1. クリーン起動（localStorage削除）→ スタート画面 → サンプル読込
2. 新規プロジェクト作成（J-SOX／マニュアル両用途）
3. 工程・リスク・統制の追加・編集・削除 →［反映］→ フロー図/プレビューの同期
4. JSON保存 → 再読込（開く）→ 内容一致
5. Excel/CSV取込（サンプル.xlsx生成 → 取込 → マッピング → プレビュー → 取込 → Undo）
6. ギャップチェック／ウォークスルー／ロールフォワード表示
7. Excel出力（コンテキスト／三点セット一式）・draw.io・Mermaid・PNG/SVG・印刷プレビュー
8. 評価機能オン→評価入力→オフ→データ保持→再オンで復元
9. AI回答取込：正しいJSON／壊れたJSON（エラーメッセージ）／Undo
10. スマホ幅（≤768px）でのPC推奨案内、紹介ページの表示

簡易スモーク（構文）：メインscriptを抽出して `node --check`。

## 組み込みセルフテスト（自動）

`jsox_flow_builder.html?selftest=1` を開くと、16項目の自動スモークが実行され、結果がダイアログと `window.__selftest` に出力されます（実データには影響せず、終了時に復元されます）。

対象: 新規作成／サンプル読込／JSON往復／後方互換（旧JSON）／CSV取込（正常・不正）／行の追加編集削除／三点セット同期／ID重複検出／ギャップチェック／ロールフォワード／Excel出力／draw.io出力／評価オンオフとデータ保持／AI取込バリデーション（正・壊れJSON）／Excel取込マッピング

## デモ・撮影用パラメータ

`jsox_flow_builder.html?pg=<page>&demo=<ai|aiimport|xls|tmpl|map>` でサンプルデータの特定画面を直接表示（スクリーンショット用・通常利用に影響なし）。

## アーカイブ

`docs/archive/` に初期デザインモック（dc.html＋support.js）・実装反映ガイド・旧スクリーンショットを保全。
