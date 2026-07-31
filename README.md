<p align="center"><img src="assets/og/og.png" alt="J-SOX Flow Builder — J-SOX三点セットを、ひとつのデータから" width="720"></p>

# J-SOX Flow Builder

**バラバラのExcelで管理されているJ-SOX三点セットを、一つの構造化データから作成・更新できる無料ツールです。**
AIで作成したRCM案等も取り込み、人間が確認・確定したうえで、業務記述書、フロー図、RCM、Excel、draw.io等へ出力できます。

> 🚀 **紹介ページ（スマホOK）** → https://norimaki-audit.github.io/jsox-flow-builder/
> 💻 **アプリを開く（PC推奨）** → https://norimaki-audit.github.io/jsox-flow-builder/jsox_flow_builder.html

| Status | Version | Tested | Self-test | Last verified |
|---|---|---|---|---|
| **Beta** | v0.9.0-beta | Chrome / Edge | **18項目**（`?selftest=1` で誰でも実行可） | 2026-08-01 |

- 📦 [出力される成果物サンプル](https://norimaki-audit.github.io/jsox-flow-builder/#outputs)（Excel / PDF / draw.io / SVG / JSON — 実出力）
- 🎬 [操作の流れ（デモ）](https://norimaki-audit.github.io/jsox-flow-builder/#demo)
- 🐛 [不具合報告・要望はこちら](https://github.com/norimaki-audit/jsox-flow-builder/issues/new/choose)
- ⚠️ 既知の制約: スマホでの編集操作は非対応（閲覧案内を表示）／証憑フォルダ格納は Chrome・Edge のみ／Excelの複雑な結合セルは取込時に列マッピングでの調整が必要

- 💻 PC推奨（横長の表・フロー図を扱うため）
- 📦 インストール不要・アカウント不要
- 🔒 入力した業務データをアプリから外部送信しない（ローカル処理）
- 📥 既存Excel／CSVからの取込に対応
- 📤 Excel／draw.io／PDF等への出力に対応
- 🤖 AI相談用データの生成・AI回答の構造化取込に対応

## 3つの主要価値

1. **三点セットの一元管理** — 工程・リスク・統制を構造化データとして管理し、業務記述書・フロー図・RCMを**矛盾のない状態で同期生成・更新**。修正のたびに3ファイルを直す作業から解放されます
2. **既存Excelからの移行** — 各社様式のExcel/CSVを列マッピングで取込。マッピング設定は保存して再利用できます
3. **AI時代の分業設計** — AIは下書き・レビュー、本ツールは構造・整合・確定・出力、人間は判断と責任。AI回答は差分プレビューを確認してから取り込みます

## 実際の操作画面

| | |
|---|---|
| ![開始方法の選択](assets/screenshots/current/01-start-options.png) | ![業務記述書の編集](assets/screenshots/current/02-steps-edit.png) |
| 開始は3択（取込／テンプレート／サンプル） | 業務記述書：1行＝1工程 |
| ![自動生成フロー図](assets/screenshots/current/03-flow-generated.png) | ![AI回答の取込プレビュー](assets/screenshots/current/07-ai-import-preview.png) |
| フロー図は自動生成（JIS記号・R/Cタグ） | AI回答は差分を確認してから取込 |

→ その他の画面は[紹介ページ](https://norimaki-audit.github.io/jsox-flow-builder/#shots)へ

## 基本的な利用フロー

```
入力・取込（Excel/CSV・テンプレート・サンプル）
  ↓
内容確認・修正（工程 ⇄ リスク・統制の関連付け）
  ↓
三点セット生成（業務記述書・フロー図・RCM が同期）
  ↓
Excel／draw.io／PDF等へ出力
```

## AIとの役割分担

| 担当 | 役割 |
|---|---|
| AI | 下書き、文章改善、リスク候補、網羅性確認、壁打ち |
| 本ツール | **構造化、三点セット間の整合、保存、差分確認、成果物出力** |
| 人間 | 内容確認、判断、修正、承認、最終責任 |

AIへの送信は自動では行いません。ツール内で相談用データを生成 → 利用者が任意のAIへ貼り付け → 回答を貼り戻すと**取込内容をプレビュー**し、確定した内容だけが正式データに反映されます（Undo可）。

## PCでの始め方

1. [アプリを開く](https://norimaki-audit.github.io/jsox-flow-builder/jsox_flow_builder.html)（Chrome / Edge / Firefox / Safari）
2. 開始画面で「サンプルデータで試す」を選択（まずはこれがおすすめ）
3. 慣れたら「既存Excel/CSVを取り込む」または「テンプレートから新規作成」で自社データへ

`jsox_flow_builder.html` をダウンロードしてダブルクリックでも動作します（オフライン時はフォント・アイコンが簡易表示）。

## データ・プライバシー

- 入力した業務データは、アプリから外部サーバーへ**送信しません**（ブラウザ内で処理）
- 画面表示用のフォント・アイコン等はCDNから取得します（入力データとは無関係です）
- 作業内容はブラウザに自動保存（2世代）され、**プロジェクト保存(.json)** でPCに恒久保存・復元できます
- 詳細は [docs/PRIVACY.md](docs/PRIVACY.md)

## 主な出力形式

装飾付きExcel（フロー図込み）／値のみExcel／CSV／draw.io／Mermaid／PNG・SVG／印刷・PDF（監査調書スタイル）

<details>
<summary>評価管理等のオプション機能（初期状態では非表示）</summary>

ファイルメニューの「評価・証憑管理機能」をオンにすると利用できます。オフでもデータは保持されます。

- 整備・運用評価（評価主体・手続種類・査閲欄つき）
- サンプリング調書（1統制1葉・サンプル別結果・例外自動集計）
- 評価結果一覧
- 不備管理
- 証憑管理（ブラウザ内格納／PCフォルダ格納）

また「業務マニュアルモード」に切り替えると、J-SOX評価を使わない手順書＋業務フロー図の作成ツールとして利用できます。

</details>

## 制約・免責

- ベータ版・開発中です。バックアップとして .json 保存をご活用ください
- 本ツールは内部統制文書の作成を支援するものであり、特定の様式・監査対応を保証するものではありません。実際の評価・開示にあたっては、金融庁「財務報告に係る内部統制の評価及び監査の基準」等をご確認ください
- スマートフォンでは概要閲覧を想定しています（操作はPC推奨）

## リポジトリ構成

| パス | 内容 |
|---|---|
| `jsox_flow_builder.html` | アプリ本体（単一HTML・これ1つで動作） |
| `index.html` | 紹介ページ（スマホ対応） |
| `assets/` | スクリーンショット・OG画像 |
| `docs/` | 利用ガイド・プライバシー・開発資料アーカイブ |
| `CHANGELOG.md` | 更新履歴 |

## 開発状況

公認会計士が実務経験をもとに、AI（Claude Code）を活用して開発しています。現在も操作性・出力・AI連携を改善中です。ご意見・不具合報告は [Issues](https://github.com/norimaki-audit/jsox-flow-builder/issues) へ。

## ライセンス

**利用は無料**（社内業務・商用の業務での利用を含む）。作成した成果物の権利は利用者に帰属します。
ソースコードの再配布・派生ツールの公開・他製品への組み込みは**事前の許諾が必要**です。詳細は [LICENSE.md](LICENSE.md) をご覧ください。
