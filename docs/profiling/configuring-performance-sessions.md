---
title: パフォーマンス セッションの構成 | Microsoft Docs
description: 必要なパフォーマンス データを収集するように Visual Studio プロファイリング ツールを構成する方法について学習します。 この記事では、一般的なタスクの一覧を示し、リンクを提供します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- common tasks, performance
- common tasks, profiling tools
- profiling tools, common tasks
- performance, gathering data
ms.assetid: e1c3ba41-ffca-4edf-9a7f-8a5a9244ef9b
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 52e2575e034dbabe5e380857edd95e4bc46f56d2
ms.sourcegitcommit: 18729d7c99c999865cc2defb17d3d956eb3fe35c
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 01/23/2021
ms.locfileid: "98721022"
---
# <a name="configure-performance-sessions"></a>パフォーマンス セッションの構成
[!INCLUDE[vsprvs](../code-quality/includes/vsprvs_md.md)] のプロファイリング ツールを使用して、多くの種類のアプリケーションのさまざまなパフォーマンス データを収集することができます。 このセクションでは、パフォーマンス ウィザードおよびパフォーマンス セッションとターゲット バイナリのプロパティを使用して、対象のデータを収集するようにプロファイリング ツールを構成する方法を示します。 プロファイリングを実行して収集するデータの量を制御するために、プロファイリング ツールの構成プロパティも使用できます。 詳しくは、「[データ コレクションの制御](../profiling/controlling-data-collection.md)」をご覧ください。

> [!NOTE]
> 多くの場合、パフォーマンス ウィザードの既定のプロパティを使用することは、プロファイル データを収集する効果的な方法です。 詳細については、[パフォーマンス プロファイリングのビギナーズ ガイド](../profiling/beginners-guide-to-performance-profiling.md)および[概要](../profiling/getting-started-with-performance-tools.md)に関する記事をご覧ください。

## <a name="common-tasks"></a>一般的なタスク

| タスク | 関連コンテンツ |
| - | - |
| **基本のプロファイリング オプションを設定する:** Microsoft シンボル サーバーを使用するように [!INCLUDE[vs_current_short](../code-quality/includes/vs_current_short_md.md)] を構成する必要があります。 そうすることにより、現在のバージョンの Windows や他の Microsoft アプリケーションで、関数名やパラメーター名などのシンボルへのアクセスを確保できます。 プロファイリング セッションが開始する前に、プロファイリング ツールへのシステムのアクセス許可やプロファイル データ ファイルの名前など、他の一般的なオプションを指定することもできます。 | -   [方法: Windows シンボル情報を参照する](../profiling/how-to-reference-windows-symbol-information.md)<br />-   [方法: シンボル情報をシリアル化する](../profiling/how-to-serialize-symbol-information.md)<br />-   [方法: 現在のセッションを設定する](../profiling/how-to-set-the-current-session.md)<br />-   [方法: アクセス許可を設定する](../profiling/how-to-set-permissions.md)<br />-   [方法: パフォーマンス データ ファイル名のオプションを設定する](../profiling/how-to-set-performance-data-file-name-options.md) |
| **収集するデータを指定する:** プロファイリング セッションの構成に使用する手順は、プロファイル対象のアプリケーションの種類および収集するパフォーマンス データの種類によって異なります。 | -   [方法: 収集方法を選択する](../profiling/how-to-choose-collection-methods.md)<br />-   [サンプリングを使用したパフォーマンス統計情報の収集](../profiling/collecting-performance-statistics-by-using-sampling.md)<br />-   [.NET メモリの割り当てと有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)<br />-   [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)<br />-   [方法: Web ページ内の JavaScript コードをプロファイリングする](../profiling/how-to-profile-javascript-code-in-web-pages.md)<br />-   [スレッドとプロセスのコンカレンシー データの収集](../profiling/collecting-thread-and-process-concurrency-data.md)<br />-   [追加のパフォーマンス データの収集](../profiling/collecting-additional-performance-data.md) |
| **高度な構成オプションを設定する:** 共通言語ランタイム (CLR) の複数のバージョンを読み込む .NET Framework アプリケーションに対してプロファイルを行う場合は、プロファイル対象のバージョンを指定できます。 パフォーマンス セッションに複数の .exe ファイルがある場合は、バイナリの開始順序を設定できます。 | -   [方法: .NET Framework ランタイムを指定する](../profiling/how-to-specify-the-dotnet-framework-runtime.md)<br />-   [方法: 開始するバイナリを指定する](../profiling/how-to-specify-the-binary-to-start.md) |

## <a name="related-sections"></a>関連項目
- [データ収集の制御](../profiling/controlling-data-collection.md)

## <a name="see-also"></a>関連項目
- [パフォーマンス エクスプローラー](../profiling/performance-explorer.md)
