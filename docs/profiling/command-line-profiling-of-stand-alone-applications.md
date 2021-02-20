---
title: スタンドアロン アプリケーションのコマンド ラインによるプロファイリング | Microsoft Docs
description: コマンド ラインからプロファイル ツールを使用して、クライアント (スタンドアロン) アプリケーションのパフォーマンス データを収集する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- profillng tools,stand-alone applications
- profling stand-alone applications
ms.assetid: a47f2bf2-186d-4120-bb79-34e2f3a1ee42
author: mikejo5000
ms.author: mikejo
manager: jmartens
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 583fa649b4628aa3af28f1fa7368da4de64684fa
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99969465"
---
# <a name="command-line-profiling-of-stand-alone-applications"></a>スタンドアロン アプリケーションのコマンド ラインによるプロファイリング
このセクションでは、コマンド ラインから [!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] プロファイリング ツールを使用して、スタンドアロン (クライアント) アプリケーションのパフォーマンス データを収集する手順とオプションについて説明します。

## <a name="common-tasks"></a>一般的なタスク

| タスク | 関連コンテンツ |
| - | - |
| **アプリケーションの統計情報を収集する:** サンプリング メソッドを使用してパフォーマンスの統計情報を収集します。 サンプリング データは、CPU 使用率の問題を分析し、アプリケーションの全般的なパフォーマンス特性を理解する際に役立ちます。 | -   [サンプリングを使用したアプリケーション統計情報の収集](../profiling/collecting-application-statistics-for-stand-alone-applications.md) |
| **詳細なタイミング データの収集:** インストルメンテーション メソッドを使用して詳細なタイミング情報を収集します。 インストルメンテーション データは、I/O の問題を分析し、アプリケーション シナリオを詳しく分析する場合に役立ちます。 | -   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-for-a-stand-alone-application.md) |
| **.NET メモリ データの収集:** サンプリングまたはインストルメンテーションを使用して .NET メモリ割り当てデータを収集し、割り当てられているオブジェクトのサイズと数を表示します。 また、オブジェクトのサイズと数を表示するオブジェクト有効期間期間も収集できます。この情報は各ガベージ コレクションの生成で解放されます。 | -   [.NET Framework メモリ データの収集](../profiling/collecting-dotnet-framework-memory-data-for-stand-alone-applications.md) |
| **コンカレンシー データの収集:** コンカレンシー メソッドを使用すると、リソース競合データとスレッド アクティビティ データを収集し、CPU 使用率、スレッド競合、スレッドの移行、同期の遅延、重複 I/O の領域などのシステム イベントを表示できます。 | -   [コンカレンシー データの収集](../profiling/collecting-concurrency-data-for-stand-alone-applications.md) |
| **階層の相互作用データの追加:** アプリケーションから Microsoft [!INCLUDE[ssNoVersion](../data-tools/includes/ssnoversion_md.md)] データベースに対する同期 ADO.NET 呼び出しに関するパフォーマンス データを追加できます。 プロファイリングの実行に階層の相互作用データを追加するには、コマンド ライン プロファイリング ツールによる特定の手順が必要です。 | -   [階層相互作用データを収集する](../profiling/adding-tier-interaction-data-from-the-command-line.md) |

## <a name="related-tasks"></a>関連タスク

|タスク|関連するコンテンツ|
|----------|---------------------|
|**ASP.NET アプリケーションのプロファイリング**|-   [ASP.NET Web アプリケーションのプロファイリング](../profiling/command-line-profiling-of-aspnet-web-applications.md)|
|**サービスのプロファイリング**|-   [サービスのプロファイリング](../profiling/command-line-profiling-of-services.md)|
