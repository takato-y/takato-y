# 山田貴斗（itdoor）｜業務自動化と小さな業務システムの開発

業務の手作業を減らす自動化と、社内で使う小さな業務システム（申請・承認、受注の管理、売上の集計など）を作っています。中小企業の、Excel・メール・紙で回している定型業務を主な対象としています。

毎月の集計・帳票づくり、問い合わせメールの仕分け、申請の承認、Web からの情報収集などを自動化します。使う道具は、業務の内容と社内の環境（Microsoft 365 か Google Workspace か、など）に合わせて選びます。

下のリポジトリは、作り方と品質の基準を見ていただくためのポートフォリオです。実際の案件ではなく、データもすべて架空のサンプルです（実在の企業・人物とは関係ありません）。ご相談の流れは、[ページの最後](#ご相談の流れ)にまとめています。

## ポートフォリオ

| リポジトリ | できること | 主な技術 |
|---|---|---|
| [order-intake-system](https://github.com/takato-y/order-intake-system) | 受注メールを生成AIで読み取って登録し、月末に顧客別・商品別の集計と Excel の帳票まで作る | n8n・生成AI・Python（FastAPI）・SQLite（SQL Server 用の定義も用意）・Excel VBA・Docker |
| [gas-approval-workflow](https://github.com/takato-y/gas-approval-workflow) | Google フォームの申請を金額に応じた承認者へ回し、なりすましを防ぐリンクで承認・却下する（Google 上では主な流れを確認済み） | Google Apps Script（TypeScript）・HTML |
| [rag-document-qa](https://github.com/takato-y/rag-document-qa) | 社内規程・マニュアルから根拠つきで答え、書かれていないことには答えない AI 検索チャット | Python（FastAPI）・TypeScript・ローカル LLM（Ollama） |
| [sales-dashboard-streamlit](https://github.com/takato-y/sales-dashboard-streamlit) | 売上 CSV を読み込み、売上・粗利・前年同月比・ABC 分析を表示して Excel・印刷用ページに出力する | Python・SQL（SQLite）・Streamlit |
| [web-data-collector](https://github.com/takato-y/web-data-collector) | Web の価格・在庫を robots.txt を守って定期収集し、変化を Excel とチャットへの通知で知らせる | TypeScript（Playwright）・Python・PowerShell |
| [n8n-ai-mail-triage](https://github.com/takato-y/n8n-ai-mail-triage) | 問い合わせメールを生成AIで分類し、要点の抽出・担当の振り分け・返信の下書きまで行う | n8n・生成AI |
| [excel-vba-report-automation](https://github.com/takato-y/excel-vba-report-automation) | 月別の売上ファイル（CSV・Excel）をボタン1つで取りまとめ、集計帳票と PDF を作る | Excel VBA |
| [windows-automation-scripts](https://github.com/takato-y/windows-automation-scripts) | ファイルの仕分け・定期実行の登録・CSV の整形・ログの集計を行う Windows 業務の自動化ツール集 | PowerShell・Python |

## 画面の様子

売上分析と AI 検索は、実際に起動して撮影しました。売上集計レポートは、サンプルデータで Excel のマクロを実際に動かした結果です。承認画面は、Google 環境ではなく手元のブラウザで描画したものです。各リポジトリの動作確認の範囲は、それぞれの README に書いています。

### 売上分析ダッシュボード（[sales-dashboard-streamlit](https://github.com/takato-y/sales-dashboard-streamlit)）

<img src="https://raw.githubusercontent.com/takato-y/sales-dashboard-streamlit/main/docs/images/demo.gif" alt="売上分析ダッシュボードの操作の様子" width="720">

### AI 検索チャット（[rag-document-qa](https://github.com/takato-y/rag-document-qa)）

<img src="https://raw.githubusercontent.com/takato-y/rag-document-qa/main/docs/images/demo.gif" alt="AI 検索チャットの操作の様子" width="720">

### 売上集計レポート（[excel-vba-report-automation](https://github.com/takato-y/excel-vba-report-automation)。Excel の実行結果）

<img src="https://raw.githubusercontent.com/takato-y/excel-vba-report-automation/main/docs/images/report.png" alt="売上集計レポートの帳票（集計サマリー、顧客別・月別売上、商品別売上）" width="720">

### 承認画面（[gas-approval-workflow](https://github.com/takato-y/gas-approval-workflow)。スマートフォンの画面幅）

<img src="https://raw.githubusercontent.com/takato-y/gas-approval-workflow/main/docs/images/demo.gif" alt="承認画面の操作の様子" width="300">

## どのリポジトリでもそろえていること

ご依頼いただいた場合も、使い方とトラブル時の対応手順の文書、動作を確認した範囲、変更の履歴が残ります。

- **設計書を Markdown で管理**：要件定義・基本設計・詳細設計・テスト仕様書・導入と運用の手順書・障害対応手順書に加え、その作り方を選んだ理由の記録（ADR）を残しています。要件・機能・テストに番号を振って対応づけ、どの要件をどのテストで確認したかを追えるようにしています。
- **障害が起きたときの手順まで用意**：エラーごとに、影響・切り分け・対処・復旧の確認・やり直してよいかを書いています。設計書のエラーと手順書が食い違わないよう、自動テストで突き合わせています。
- **自動テスト（CI）**：main ブランチへの反映（push）やプルリクエストのたびに、GitHub Actions で自動テスト、またはプログラムを動かさずに行う検査を実行しています。各 README には「GitHub Actions で検査している範囲」と「手元の環境でのみ確認した範囲」を分けて書き、まだ確認していないことはその旨を明記しています。
- **安全の基本**：パスワードや API キーをリポジトリに置かないことを全体の前提とし、題材に応じた対策も最初から入れています（例：社外から接続できないようにする、Excel で開いたときに入力値が計算式として動かないようにする、承認リンクに偽造防止の署名と期限を付ける）。
- **変更の記録**：機能ごとに分けて開発してから取り込み、版ごとに変更点の一覧（CHANGELOG）と公開版（Release）を残しています。

## ご相談の流れ

1. **ご相談**：プロフィール欄の Web サイトからご連絡ください。今の作業の進め方と、お困りのことをお聞きします。
2. **内容の確認**：今お使いの Excel・メール・帳票の様子をお聞きし、自動化できる範囲を整理します。
3. **お見積り**：作るものと、費用・期間をお示しします。料金の目安は[料金ページ](https://www.itdoor.jp/pricing/)をご覧ください。
4. **作成**：設計書をもとに作成し、動作を確認してからお渡しします。
5. **納品**：使い方と、トラブル時の対応手順の文書をお付けします。
