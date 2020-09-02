---
title: スタンドアロン アプリケーションのコマンド ラインによるプロファイリング | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- profillng tools,stand-alone applications
- profling stand-alone applications
ms.assetid: a47f2bf2-186d-4120-bb79-34e2f3a1ee42
caps.latest.revision: 21
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 3f4b2b78f7187b7a49b78312a1105a2af884fda3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68186634"
---
# <a name="command-line-profiling-of-stand-alone-applications"></a>スタンドアロン アプリケーションのコマンド ラインによるプロファイリング
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

このセクションでは、コマンド ラインから [!INCLUDE[vsprvs](../includes/vsprvs-md.md)] プロファイリング ツールを使用して、スタンドアロン (クライアント) アプリケーションのパフォーマンス データを収集する手順とオプションについて説明します。  
  
## <a name="common-tasks"></a>一般的なタスク  
  
|タスク|関連コンテンツ|  
|----------|---------------------|  
|**アプリケーションの統計情報を収集する:** サンプリング メソッドを使用してパフォーマンスの統計情報を収集します。 サンプリング データは、CPU 使用率の問題を分析し、アプリケーションの全般的なパフォーマンス特性を理解する際に役立ちます。|-   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**詳細なタイミング データの収集:** インストルメンテーション メソッドを使用して詳細なタイミング情報を収集します。 インストルメンテーション データは、I/O の問題を分析し、アプリケーション シナリオを詳しく分析する場合に役立ちます。|-   [インストルメンテーションを使用した詳細なタイミングデータの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application-by-using-the-profiler-command-line.md)|  
|**.NET メモリ データの収集:** サンプリングまたはインストルメンテーションを使用して .NET メモリ割り当てデータを収集し、割り当てられているオブジェクトのサイズと数を表示します。 また、オブジェクトのサイズと数を表示するオブジェクト有効期間期間も収集できます。この情報は各ガベージ コレクションの生成で解放されます。|-   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**コンカレンシー データの収集:** コンカレンシー メソッドを使用すると、リソース競合データとスレッド アクティビティ データを収集し、CPU 使用率、スレッド競合、スレッドの移行、同期の遅延、重複 I/O の領域などのシステム イベントを表示できます。|-   [同時実行データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications-by-using-the-profiler-command-line.md)|  
|**階層の相互作用データの追加:** アプリケーションから Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] データベースに対する同期 ADO.NET 呼び出しに関するパフォーマンス データを追加できます。 プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。|-   [階層相互作用データの収集](../profiling/adding-tier-interaction-data-from-the-command-line.md)|  
|**試す**: サンプリング メソッドまたはインストルメンテーション メソッドを使用してサンプル クライアント アプリケーションをプロファイリングする手順を実行します。|-   [チュートリアル: サンプリングを使ったコマンド ライン プロファイリング](../profiling/walkthrough-command-line-profiling-using-sampling.md)<br />-   [チュートリアル: インストルメンテーションを使用したコマンドラインプロファイリング](../profiling/walkthrough-command-line-profiling-using-instrumentation.md)|  
  
## <a name="related-tasks"></a>Related Tasks  
  
|タスク|関連するコンテンツ|  
|----------|---------------------|  
|**ASP.NET アプリケーションのプロファイリング**|-   [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)|  
|**サービスのプロファイリング**|-   [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)|
