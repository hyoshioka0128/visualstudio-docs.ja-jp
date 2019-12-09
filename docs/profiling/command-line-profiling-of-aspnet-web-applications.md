---
title: ASP.NET Web アプリケーションのコマンド ライン プロファイリング | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profiling ASP.NET applications
- profling tools,ASP.NET applications
ms.assetid: 897c00d5-5767-433b-a960-4a29c6023ede
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- aspnet
ms.openlocfilehash: aa184667e5d569bc2662052a29b25bfea6e470a7
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74779572"
---
# <a name="command-line-profiling-of-aspnet-web-applications"></a>ASP.NET Web アプリケーションのコマンド ライン プロファイリング
このセクションでは、コマンド ラインから [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールを使用して、[!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションのパフォーマンス データを収集する手順とオプションについて説明します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="common-tasks"></a>一般的なタスク

| タスク | 関連するコンテンツ |
| - | - |
| **ASP.NET プロファイリング データを簡単に収集する:** **VSPerfASPNETCmd** ツールを使用して、サンプリング、インストルメンテーション、.NET メモリ、競合、または階層の相互作用データを収集できます。**VSPerfCmd** の場合は必要ですが、構成の要件とインターネット インフォメーション サービス (IIS) の再起動は必要ありません。 **VSPerfASPNETCmd** では、追加のデータ収集またはコントロール データの収集を使用できません。 **注:** **VSPerfASPNETCmd** は、スタンドアロン プロファイラーを使用して ASP.NET Web サイトをプロファイリングする場合に推奨されます。 | -   [VSPerfASPNETCmd を使用した迅速な Web サイト プロファイリング](../profiling/rapid-web-site-profiling-with-vsperfaspnetcmd.md) |
| **アプリケーション統計情報の収集:** サンプリング メソッドを使用してパフォーマンスの統計情報を収集します。 サンプリング データは、CPU 使用率の問題を分析し、アプリケーションの全般的なパフォーマンス特性を理解する際に役立ちます。 | -   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-aspnet-using-the-profiler-sampling-method.md) |
| **詳細なタイミング データの収集:** インストルメンテーション メソッドを使用して詳細なタイミング情報を収集します。 インストルメンテーション データは、I/O の問題を分析し、アプリケーション シナリオを詳しく分析する場合に役立ちます。 | -   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-aspnet-profiler-instrumentation-method.md) |
| **.NET メモリ データの収集:** サンプリングまたはインストルメンテーションを使用して .NET メモリ割り当てデータを収集し、割り当てられているオブジェクトのサイズと数を表示します。 また、オブジェクトのサイズと数を表示するオブジェクト有効期間期間も収集できます。この情報は各ガベージ コレクションの生成で解放されます。 | -   [メモリ データの収集](../profiling/collecting-memory-data-from-an-aspnet-web-application.md) |
| **コンカレンシー データの収集:** 同時実行メソッドを使用してリソースの競合データを収集します。 **注:** スレッド アクティビティと視覚化データの収集は、Web アプリケーションではサポートされません。 | -   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-an-aspnet-web-application.md) |
| **階層の相互作用データを追加する:** [!INCLUDE[vstecasp](../code-quality/includes/vstecasp_md.md)] Web アプリケーションから Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] データベースに対する同期 [!INCLUDE[vstecado](../data-tools/includes/vstecado_md.md)] 呼び出しに関するパフォーマンス データを追加できます。 | -   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md) |

## <a name="related-tasks"></a>関連するタスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**スタンドアロン (クライアント) アプリケーションのプロファイリング**|-   [スタンドアロン アプリケーションのプロファイリング](../profiling/command-line-profiling-of-stand-alone-applications.md)|
|**サービスのプロファイリング**|-   [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)|
