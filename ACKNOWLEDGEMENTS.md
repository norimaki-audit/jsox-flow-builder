# 謝辞（ACKNOWLEDGEMENTS）

## 着想元

本プロジェクトの開発のきっかけの一つは、兎耳山ルカ氏（tomiyamaluca）の次のプロジェクト・記事です。

- リポジトリ: [tomiyamaluca/CC_Internal_Control](https://github.com/tomiyamaluca/CC_Internal_Control)（MIT License）
- 内容: Claude Code を用いて内部統制三点セット（業務記述書・業務フロー図・RCM）を drawio 形式まで一括生成する試み

「AIで三点セットを生成する」という発想から大きな刺激を受けました。この場を借りて感謝します。

## 本プロジェクトとの関係

J-SOX Flow Builder は、生成された後の**編集・保存・Excel取込・整合チェック・評価・証憑・不備管理**までを扱うことを目的に、単一HTMLのWebアプリとして**独自に実装**したものです。

両プロジェクトを比較のうえ確認した結果、CC_Internal_Control のコード、プロンプト（CLAUDE.md）、Markdown/drawioテンプレート、サンプルデータからの**具体的な流用はありません**（本プロジェクトのデータモデル・列構成・サンプルプロセス・drawio出力はいずれも独自実装です）。本プロジェクトは同プロジェクトの派生物ではなく、公式・非公式を問わず関係を示すものでもありません。
