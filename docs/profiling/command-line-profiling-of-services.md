---
title: サービスのコマンド ライン プロファイリング | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling toos,services
- profiling services
ms.assetid: f0d62318-b0e8-49c6-9a30-9f7a6adef2f6
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: b20835eaf8b81bd64bd90aa75d2efb32975a7c53
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74772832"
---
# <a name="command-line-profiling-of-services"></a>サービスのコマンド ライン プロファイリング
このセクションでは、コマンド ラインから [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールを使用して、Windows サービスのパフォーマンス データを収集する手順とオプションについて説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

| タスク | 関連するコンテンツ |
| - | - |
| **アプリケーション統計情報の収集:** サンプリング メソッドを使用してパフォーマンスの統計情報を収集します。 サンプリング データは、CPU 使用率の問題を分析し、アプリケーションの全般的なパフォーマンス特性を理解する際に役立ちます。 | -   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-services-by-using-the-profiler-sampling-method.md) |
| **詳細なタイミング データの収集:** インストルメンテーション メソッドを使用して詳細なタイミング情報を収集します。 インストルメンテーション データは、I/O の問題を分析し、アプリケーション シナリオを詳しく分析する場合に役立ちます。 | -   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-services-by-using-the-instrumentation-method.md) |
| **.NET メモリ データの収集:** サンプリングまたはインストルメンテーションを使用して .NET メモリ割り当てデータを収集し、割り当てられているオブジェクトのサイズと数を表示します。 また、オブジェクトのサイズと数を表示するオブジェクト有効期間期間も収集できます。この情報は各ガベージ コレクションの生成で解放されます。 | -   [.NET メモリ データの収集](../profiling/collecting-memory-data-from-dotnet-framework-services-by-using-the-profiler-command-line.md) |
| **コンカレンシー データの収集:** コンカレンシー メソッドを使用すると、リソース競合データとスレッド アクティビティ データを収集し、CPU 使用率、スレッド競合、スレッドの移行、同期の遅延、重複 IO の領域などのシステム イベントを表示できます。 | -   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-a-service-by-using-the-profiler-command-line.md) |
| **階層の相互作用データを追加する:** サービスから Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] データベースに対する同期 ADO.NET 呼び出しに関するパフォーマンス データを追加できます。 | -   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md) |

## <a name="related-tasks"></a>関連するタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)|
|**ASP.NET アプリケーションのプロファイリング**|-   [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)|
