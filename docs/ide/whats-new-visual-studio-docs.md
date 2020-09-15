---
title: 'Visual Studio のドキュメント:2020 年 8 月の新機能 '
titleSuffix: ''
description: 2020 年 8 月の Visual Studio ドキュメントの最新情報。
ms.date: 09/02/2020
helpviewer_keywords:
- Visual Studio, what's new, docs
- what's new [Visual Studio]
ms.assetid: 89844796-621B-4EF5-9D76-197084B011CB
author: JoshuaPartlow
ms.author: joshuapa
manager: jillfra
ms.prod: visual-studio-windows
ms.technology: vs-ide-general
ms.topic: conceptual
ms.workload:
- multiple
ms.openlocfilehash: 4364bd62ac19be958632b8cb2dbbe907013e8a70
ms.sourcegitcommit: 703c68667261df5985a73282c1cbb0541118989c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "89402245"
---
# <a name="visual-studio-docs-whats-new-for-august-2020"></a>Visual Studio のドキュメント:2020 年 8 月の新機能

2020 年 8 月の Visual Studio ドキュメントの最新情報へようこそ。 この記事では、この期間中にドキュメントに加えられた大きな変更の一部を一覧で示します。 以前の月の新機能については、[新機能の履歴](whats-new-visual-studio-docs-history.md)に関するトピックを参照してください。

## <a name="azure"></a>Azure

**新しい記事**

- [Visual Studio 接続済みサービスを使用して Azure Application Insights を追加する](/visualstudio/azure/azure-app-insights-add-connected-service) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure Cache for Redis を追加する](/visualstudio/azure/azure-cache-for-redis-add-connected-service) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure Cosmos DB をアプリに追加する](/visualstudio/azure/azure-cosmosdb-add-connected-service) - VS 2019 16.7 の接続済みサービス
- [Visual Studio 接続済みサービスを使用して Azure SignalR を追加する](/visualstudio/azure/azure-signalr-add-connected-service) - VS 2019 16.7 の接続済みサービス
- [Azure SQL Database への接続を追加する](/visualstudio/azure/azure-sql-database-add-connected-service) - VS 2019 16.7 の接続済みサービス

**更新された記事**

- [Visual Studio 接続済みサービスを使用した Azure ストレージの追加](/visualstudio/azure/vs-azure-tools-connected-services-storage)
  - VS 2019 16.7 の接続済みサービス
  - Azure Storage 接続済みサービスの記事: UI およびサポートされているプロジェクトの種類の更新

## <a name="code-quality"></a>コード品質

**新しい記事**

- [CA1310: 正確さのために StringComparison を指定する](/visualstudio/code-quality/ca1310) - CA1310 のドキュメントを追加、CA1307 のドキュメントを更新
- [CA1837: Process.GetCurrentProcess().Id の代わりに Environment.ProcessId を使用する](/visualstudio/code-quality/ca1837) - CA1837 のドキュメント
- [CA1838: P/Invoke に対して `StringBuilder` パラメーターを使用しない](/visualstudio/code-quality/ca1838) - CA1838 のドキュメントを追加
- [CA2008: TaskScheduler を渡さずにタスクを作成しない](/visualstudio/code-quality/ca2008) - CA2008 のドキュメントを追加
- [CA2249: String.IndexOf の代わりに String.Contains を使用することを検討する](/visualstudio/code-quality/ca2249) - CA2249 のドキュメント
- [CA2361: DataSet.ReadXml() を含む自動生成クラスが信頼されていないデータで使用されていないことを確認する](/visualstudio/code-quality/ca2361) - DataSet/DataTable の規則の追加
- [CA2362: シリアル化可能な自動生成型の安全でない DataSet または DataTable は、リモート コード実行攻撃に対して脆弱になる可能性がある](/visualstudio/code-quality/ca2362) - DataSet/DataTable の規則の追加
- [IL3000: 単一ファイルとして発行するときにアセンブリ ファイル パスへのアクセスを使用しない](/visualstudio/code-quality/il3000) - IL3000 のドキュメントを追加
- [IL3001: 単一ファイルとして発行するときにアセンブリ ファイル パスにアクセスしない](/visualstudio/code-quality/il3001) - IL3001 のドキュメントを追加

**更新**

- [CA1002: ジェネリック リストを公開しない](/visualstudio/code-quality/ca1002) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1046: 参照型で演算子 equals をオーバーロードしない](/visualstudio/code-quality/ca1046) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1307: 明確化のために StringComparison を指定する](/visualstudio/code-quality/ca1307) - CA1310 のドキュメントを追加、CA1307 のドキュメントを更新
- [CA1700: 列挙型の値に &#39;Reserved&#39; という名前を指定しない](/visualstudio/code-quality/ca1700) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1707: 識別子にアンダースコアを含めることはできない](/visualstudio/code-quality/ca1707) - 構成可能な項目の追加 - API サーフェス セクション
- [CA1822: メンバーを static に設定する](/visualstudio/code-quality/ca1822) - 構成可能な項目の追加 - API サーフェス セクション
- [CA2351:DataSet.ReadXml() の入力が信頼されていることを確認する](/visualstudio/code-quality/ca2351) - DataSet/DataTable の規則の追加
- [サードパーティ製アナライザーのインストール](/visualstudio/code-quality/install-roslyn-analyzers) - コード分析のドキュメントの構造とタイトルの変更

## <a name="containers"></a>コンテナー

**更新された記事**

- [Visual Studio を使用して ASP.NET Docker コンテナーをコンテナー レジストリにデプロイする](/visualstudio/containers/hosting-web-apps-in-docker) - Visual Studio 16.7 の発行 UI のコンテナー ツールの更新
- [Visual Studio Kubernetes ツールの概要](/visualstudio/containers/tutorial-kubernetes-tools) - Kubernetes チュートリアル: 削除に対する手順の追加

## <a name="deployment"></a>デプロイ

**新しい記事**

- [Visual Studio Installer Projects 拡張機能 と .NET Core 3.1](/visualstudio/deployment/installer-projects-net-core) - インストーラー プロジェクトの .NET Core 3.1 の機能に対する新しいヘルプ ページの作成

**更新された記事**

- [フォルダー、IIS、Azure、または別の場所にアプリを配置する](/visualstudio/deployment/deploying-applications-services-and-components-resources) - 配置に関する更新
- [Visual Studio での配置](/visualstudio/deployment/index) - 配置に関する更新

## <a name="extensibility"></a>機能拡張

**更新された記事**
- [プロジェクトのサブタイプ](/visualstudio/extensibility/internals/project-subtypes) - リスト項目のインデントの修正
- [Visual Studio の色の値の参照](/visualstudio/extensibility/ux-guidelines/color-value-reference-for-visual-studio) - 列ヘッダーがない AB#1759333 の修正

## <a name="get-started"></a>作業開始

**更新された記事**

- [手順 5:Azure に ASP.NET Core アプリをデプロイする](/visualstudio/get-started/csharp/tutorial-aspnet-core-ef-step-05) - 新しい接続済みサービスの UI に関するビデオ チュートリアルの更新

## <a name="ide"></a>IDE

**新しい記事**

- [Visual Studio の F1 ヘルプ キーを変更する](/visualstudio/ide/not-in-toc/change-f1-help-key) - 既定の F1 ヘルプ ページのリファクタリング
- [テキスト エディターの F1 ヘルプ](/visualstudio/ide/not-in-toc/default-f1-text-editor) - 既定の F1 ヘルプ ページのリファクタリング
- [`typeof` を `nameof` に変換](/visualstudio/ide/reference/convert-typeof-to-nameof) - typeof から nameof への変換のリファクタリング
- [LINQ 式の簡略化](/visualstudio/ide/reference/simplify-linq-expression) -LINQ 式簡略化のリファクタリング

**更新された記事**

- [Visual Studio のウィンドウ レイアウトをカスタマイズする](/visualstudio/ide/customizing-window-layouts-in-visual-studio) - 「ウィンドウ レイアウトをカスタマイズする」トピックへのモニカーされた縦型のドキュメント タブの情報の追加
- [Visual Studio または Visual Studio Installer に関する問題を報告する方法](/visualstudio/ide/how-to-report-a-problem-with-visual-studio)
  - NMI に詳細情報を追加しました
  - [問題の報告] ページ全体を再作成しました
- [F1 ヘルプ](/visualstudio/ide/not-in-toc/default) - 既定の F1 ヘルプ ページのリファクタリング
- [[自動バックアップ] ([オプション] ダイアログ ボックス - [環境])](/visualstudio/ide/reference/autorecover-environment-options-dialog-box) - 更新された自動保存ファイルの場所に関する情報の追加
- [[オプション]、[テキスト エディター]、[基本] (Visual Basic)、[詳細]](/visualstudio/ide/reference/options-text-editor-basic-visual-basic) - インライン パラメーター名のヒントに関する基本的なドキュメントの追加
- [[オプション]、[テキスト エディター]、[C#]、[詳細]](/visualstudio/ide/reference/options-text-editor-csharp-advanced) - インライン パラメーター名のヒントに関する基本的なドキュメントの追加
- [Visual Studio のパフォーマンスのヒントとテクニック](/visualstudio/ide/visual-studio-performance-tips-and-tricks) - "マップ モードの無効化" と "右端での折り返しの無効化" の情報の追加
- [Visual Studio 2019 の新機能](/visualstudio/ide/whats-new-visual-studio-2019) - 16.7 GA 情報に関する Visual Studio 2019 の新機能の更新

## <a name="rtvs"></a>RTVS

**更新された記事**

- [SQL Server と R の使用](/visualstudio/rtvs/integrating-sql-server-with-r) - 列ヘッダーを含むように表を修正

## <a name="community-contributors"></a>コミュニティの共同作成者

上記の期間中、Visual Studio ドキュメントへのご協力をいただいた方々です。 よろしくお願いいたします。 Visual Studio ドキュメントへの投稿を行う方法については、[共同作成者ガイド](https://docs.microsoft.com/contribute/)のガイダンスに従ってください。

- [AlexB-SheldonMFG](https://github.com/AlexB-SheldonMFG) - Alex Black (11)
- [Youssef1313](https://github.com/Youssef1313) - Youssef Victor (8)
- [hyoshioka0128](https://github.com/hyoshioka0128) - Hiroshi Yoshioka (3)
- [AstroChoco](https://github.com/AstroChoco) - Qian Lu (Chocolate) (1)
- [athyunnath](https://github.com/athyunnath) - Athyunnath Eleti (1)
- [caro-oviedo](https://github.com/caro-oviedo) - Caro Oviedo (1)
- [Evangelink](https://github.com/Evangelink) - Amaury Levé (1)
- [jethas-bennettjones](https://github.com/jethas-bennettjones) - Shafiq Jetha (1)
- [nebuk89](https://github.com/nebuk89) - Ben De St Paer-Gotch (1)
- [pcartwright81](https://github.com/pcartwright81) (1)
- [pkulikov](https://github.com/pkulikov) - Petr Kulikov (1)
- [riQQ](https://github.com/riQQ) (1)
- [tcmetzger](https://github.com/tcmetzger) - Timo Cornelius Metzger (1)
- [weitzhandler](https://github.com/weitzhandler) - Shimmy (1)