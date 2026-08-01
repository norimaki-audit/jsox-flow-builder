# 第三者ソフトウェア・アセットの表示（THIRD PARTY NOTICES）

本プロジェクトが利用している第三者のライブラリ・フォント・アイコンの一覧です。各ライセンスの全文は公式URLを参照してください。本ファイルは技術的な依存関係と帰属表示の整理を目的としており、法的助言ではありません。

## 同梱（jsox_flow_builder.html 内にインライン）

| ライブラリ | バージョン | ライセンス | 公式URL | 形態 |
|---|---|---|---|---|
| SheetJS Community Edition (xlsx) | 0.18.5 | Apache-2.0 | https://sheetjs.com/ / https://git.sheetjs.com/sheetjs/sheetjs | 同梱（minified） |
| ExcelJS | 4.x | MIT | https://github.com/exceljs/exceljs | 同梱（minified、依存の dayjs / fast-csv 等を含むバンドル） |

- SheetJS CE は Excel/CSV の読み取り（取込）に使用しています。
- ExcelJS は装飾付き Excel の書き出しに使用しています。
- 両ライブラリとも改変せずに同梱しています。同梱バンドルに含まれる推移的依存（dayjs ほか）は各上流のライセンス（MIT 等）に従います。

## 外部取得（CDN。ページ表示用であり、入力データは送信されません）

| アセット | バージョン | ライセンス | 公式URL | 取得元 |
|---|---|---|---|---|
| IBM Plex Sans JP / IBM Plex Mono | — | SIL OFL 1.1 | https://github.com/IBM/plex | Google Fonts |
| Inter | — | SIL OFL 1.1 | https://github.com/rsms/inter | Google Fonts |
| Phosphor Icons (web) | 2.1.1 | MIT | https://github.com/phosphor-icons/web | unpkg |

- フォント・アイコンはオフライン時には読み込まれず、システムフォント等で代替表示されます（機能への影響はありません）。

## 本体のライセンス

本体（アプリ本体・紹介ページ・ドキュメント）の利用条件は [LICENSE.md](LICENSE.md) を参照してください。
