# 第三者ソフトウェア・アセットの表示（THIRD PARTY NOTICES）

本プロジェクトが利用している第三者のライブラリ・フォント・アイコンの一覧です。これらの部分には本体の [J-SOX Flow Builder Source-Available License 1.0](../LICENSE.md) は適用されず、**それぞれの第三者ライセンスが適用されます**。各ライセンスの全文は 本ディレクトリ（licenses/）に同梱しています。本ファイルは技術的な依存関係と帰属表示の整理を目的としており、法的助言ではありません。

監査方法: `jsox_flow_builder.html` 内の同梱コード（バージョン文字列・バンドル構造）、および HTML の外部参照（`<link>`）をコードから直接確認し、著作権者表記は各公式配布元のライセンス原文から転記しています。

## 同梱（jsox_flow_builder.html 内にインライン）

| ライブラリ | バージョン | 著作権者 | ライセンス | 全文 | 公式配布元 |
|---|---|---|---|---|---|
| SheetJS Community Edition (xlsx) | 0.18.5（コード内バージョン文字列で確認） | SheetJS LLC | Apache-2.0 | [SheetJS-Apache-2.0.txt](SheetJS-Apache-2.0.txt) | https://sheetjs.com/ / https://git.sheetjs.com/sheetjs/sheetjs |
| ExcelJS | 4.x（バンドルにバージョン文字列なし。4系のUPGRADE-4.0参照を含むことから4系と判断） | Guyon Roche (c) 2014-2019 | MIT | [ExcelJS-MIT.txt](ExcelJS-MIT.txt) | https://github.com/exceljs/exceljs |

- SheetJS CE は Excel/CSV の読み取り（取込）に使用しています。
- ExcelJS は装飾付き Excel の書き出しに使用しています。
- 両ライブラリとも改変せずに minified 形態で同梱しています。
- ExcelJS のブラウザ向けバンドルには推移的依存（dayjs、fast-csv ほか）が含まれます。これらは各上流プロジェクトのライセンス（MIT 等）に従います。個別の全文は各上流リポジトリを参照してください（バンドルを改変していないため、個別分離はしていません）。

## 外部取得（CDN。ページ表示用であり、入力データは送信されません）

| アセット | バージョン | 著作権者 | ライセンス | 全文 | 取得元 |
|---|---|---|---|---|---|
| IBM Plex Sans JP / IBM Plex Mono | Google Fonts 配信の最新版 | IBM Corp. (c) 2017（Reserved Font Name "Plex"） | SIL OFL 1.1 | [IBM-Plex-OFL-1.1.txt](IBM-Plex-OFL-1.1.txt) | Google Fonts / https://github.com/IBM/plex |
| Inter | Google Fonts 配信の最新版 | The Inter Project Authors (c) 2016 | SIL OFL 1.1 | [Inter-OFL-1.1.txt](Inter-OFL-1.1.txt) | Google Fonts / https://github.com/rsms/inter |
| Phosphor Icons (web) | 2.1.1（参照URLで固定） | Phosphor Icons (c) 2020-2021 | MIT | [Phosphor-Icons-MIT.txt](Phosphor-Icons-MIT.txt) | unpkg / https://github.com/phosphor-icons/web |

- フォント・アイコンはオフライン時には読み込まれず、システムフォント等で代替表示されます（機能への影響はありません）。

## 上記以外

上記のほかに、本体コードが利用している第三者ソフトウェアはありません（ブラウザ標準API・GitHub Pages のホスティングを除く）。着想元プロジェクトについては [READMEの謝辞](../README.md#謝辞着想元) を参照してください（コード・テンプレートの流用はありません）。

## 本体のライセンス

本体（アプリ本体・紹介ページ・ドキュメント）の利用条件は [../LICENSE.md](../LICENSE.md)（J-SOX Flow Builder Source-Available License 1.0）を参照してください。
