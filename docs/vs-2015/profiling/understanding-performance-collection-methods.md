---
title: パフォーマンス収集方法について | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.performance.wizard.methodpage
helpviewer_keywords:
- Profiling Tools, profiling methods
ms.assetid: ea4881fd-bd04-4875-9b7b-28490d6706f9
caps.latest.revision: 25
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e398d7e5e297daa68663902efb8a9fa0775c86fa
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841465"
---
# <a name="understanding-performance-collection-methods"></a>パフォーマンス収集方法について
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Visual Studio プロファイリング ツールには、パフォーマンス データを収集するための 5 つの方法が用意されています。 ここでは、これらの方法について説明し、特定の方法がデータの収集方法としてどのようなシナリオに適しているのかを示します。  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
|メソッド|説明|  
|------------|-----------------|  
|[サンプリング](#sampling)|アプリケーションが実行する作業についての統計データを収集します。|  
|[インストルメンテーション](#instrumentation)|各関数呼び出しのタイミングに関する詳細情報を取得します。|  
|[コンカレンシー](#concurrency)|マルチスレッド アプリケーションに関する詳細情報を収集します。|  
|[.NET メモリ](#net_memory)|.NET メモリの割り当ておよびガベージ コレクションに関する詳細情報を収集します。|  
|[階層の相互作用](#tier_interaction)|SQL Server データベースに対する ADO.NET の同期の関数呼び出しに関する情報を収集します。<br /><br /> 階層相互作用プロファイル データは、[!INCLUDE[vsUltLong](../includes/vsultlong-md.md)]、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)]、または [!INCLUDE[vs_pro_current_short](../includes/vs-pro-current-short-md.md)] を使用して収集できます。 ただし、階層相互作用プロファイル データを表示できるのは、[!INCLUDE[vsPreLong](../includes/vsprelong-md.md)] および [!INCLUDE[vsUltLong](../includes/vsultlong-md.md)] のみです。|  
  
 一部のプロファイル方法では、ソフトウェアおよびハードウェアのパフォーマンス カウンターなど、ここで示した以外の情報も収集できます。 詳細については、「[追加のパフォーマンス データの収集](../profiling/collecting-additional-performance-data.md)」を参照してください。  
  
## <a name="sampling"></a><a name="sampling"></a> サンプリング  
 サンプリング プロファイル方式では、プロファイリング実行中にアプリケーションが実行した作業に関する統計データを収集します。 サンプリング方式は負荷が少ないため、アプリケーション メソッドの実行にほとんど影響しません。  
  
 サンプリングは、Visual Studio プロファイリング ツールの既定の方式です。 サンプリング方式は、次のような用途に適しています。  
  
- アプリケーションのパフォーマンスを初めて調査する場合  
  
- プロセッサ (CPU) の使用に関連するパフォーマンス上の問題を調査する場合  
  
  サンプリング プロファイル方式では、コンピューター プロセッサを一定の間隔で中断し、関数の呼び出し履歴を収集します。 排他サンプル カウントは、実行中の関数を対象にインクリメントされ、包括カウントは、呼び出し履歴のすべての呼び出し元関数を対象にインクリメントされます。 サンプリング レポートには、プロファイリング対象のモジュール、関数、ソース コード行、および命令について、これらのカウントの合計が表示されます。  
  
  既定では、サンプリング間隔は CPU のサイクル数に設定されます。 ただし、この間隔の種類を別の CPU パフォーマンス カウンターに変更することや、カウンター イベントの回数を間隔として設定することもできます。 また、ADO.NET 経由で行われた SQL Server データベースに対するクエリについての情報を表す階層の相互作用のプロファイル (TIP) データを収集することもできます。  
  
  [サンプリングを使用したパフォーマンス統計情報の収集](../profiling/collecting-performance-statistics-by-using-sampling.md)  
  
  [サンプリングデータ値について](../profiling/understanding-sampling-data-values.md)  
  
  [サンプリングメソッドのデータビュー](../profiling/profiler-sampling-method-data-views.md)  
  
## <a name="instrumentation"></a><a name="instrumentation"></a> 機能  
 インストルメンテーション プロファイル方式では、プロファイル対象アプリケーションにおける関数呼び出しのタイミングに関する詳細情報を収集します。 インストルメンテーション プロファイル方式は、次のような用途に適しています。  
  
- ディスク I/O などの入出力のボトルネックを調査する場合  
  
- 特定のモジュールまたは一連の関数について詳細に調査する場合  
  
  インストルメンテーション方式では、インストルメント化対象ファイル内の各関数、およびこれらの関数によって行われた各関数呼び出しのタイミングに関する情報をキャプチャするコードを、バイナリ ファイルに挿入します。 また、この方式では、関数がファイルへの書き込みなどの操作をオペレーティング システムに要求した時間も記録されます。 インストルメンテーション レポートでは、関数またはソース コード行の実行にかかった時間の合計が、次の 4 つの値を使用して表されます。  
  
- 包括経過: 関数またはソース行の実行にかかった時間の合計。  
  
- アプリケーション包括: オペレーティング システムに対する呼び出しにかかった時間を除く、関数またはソース行の実行にかかった時間。  
  
- 排他経過: 関数本体内またはソース コード行内のコードの実行にかかった時間。 関数またはソース行から呼び出された関数の実行にかかった時間は除きます。  
  
- アプリケーション排他: 関数本体内またはソース コード行内のコードの実行にかかった時間。 オペレーティング システムへの呼び出しにかかった時間、および関数またはソース行から呼び出された関数の実行にかかった時間は除きます。  
  
  インストルメンテーション方式を使用して、CPU およびソフトウェアの両方のパフォーマンス カウンターを収集することもできます。  
  
  [インストルメンテーションデータ値について](../profiling/understanding-instrumentation-data-values.md)  
  
  [インストルメンテーションを使用した詳細なタイミング データの収集](../profiling/collecting-detailed-timing-data-by-using-instrumentation.md)  
  
  [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)  
  
## <a name="concurrency"></a><a name="concurrency"></a> 多重  
 コンカレンシー プロファイルでは、マルチスレッド アプリケーションに関する情報が収集されます。 リソース競合プロファイルでは、競合するスレッドによる共有リソースへのアクセスで待機が発生するたびに、詳細な呼び出し履歴情報が収集されます。 また、コンカレンシーの視覚化では、マルチスレッド アプリケーションが、アプリケーション自体、ハードウェア、オペレーティング システム、およびホスト コンピューター上の他のプロセスと対話する方法に関する、より一般的な情報が収集されます。  
  
- リソース競合レポートには、発生した競合の合計数と、リソースに対する合計待機時間 (待機が発生したモジュール、関数、ソース コード行、命令についての合計待機時間) が表示されます。 また、タイムライン グラフにも発生した競合が表示されます。  
  
- コンカレンシー ビジュアライザーでは、パフォーマンスのボトルネック、十分に活用されていない CPU、スレッドの競合、スレッドの移行、同期の遅延、重複 I/O の領域などを特定するためのグラフィカルな情報が表示されます。 グラフィカルな出力は、呼び出し履歴とソース コードのデータにできる限りリンクされます。 コンカレンシーの視覚化データは、コマンド ラインおよび Windows アプリケーションについてのみ収集できます。  
  
  [リソース競合データ値について](../profiling/understanding-resource-contention-data-values.md)  
  
  [スレッドおよびプロセスのコンカレンシー データの収集](../profiling/collecting-thread-and-process-concurrency-data.md)  
  
  [リソース競合データビュー](../profiling/resource-contention-data-views.md)  
  
  [コンカレンシー ビジュアライザー](../profiling/concurrency-visualizer.md)  
  
## <a name="net-memory"></a><a name="net_memory"></a> .NET メモリ  
 .NET メモリ割り当てプロファイル方式では、プロファイリング対象アプリケーションで .NET Framework オブジェクトにメモリが割り当てられるたびに、コンピューター プロセッサに対して割り込みを行います。 オブジェクトの有効期間データも収集する場合は、.NET Framework のガベージ コレクションの実行後に、毎回プロファイラーがコンピューター プロセッサに対して割り込みを行います。  
  
 プロファイラーは、割り当てで作成されたオブジェクト、またはガベージ コレクションで破棄されたオブジェクトの型、サイズ、および数に関する情報を収集します。  
  
- メモリの割り当てイベントが発生すると、プロファイラーは関数の呼び出し履歴に関する追加情報を収集します。 排他的割り当てカウントは、現在実行中の関数を対象にインクリメントされ、包括的割り当てカウントは、呼び出し履歴のすべての呼び出し元関数を対象にインクリメントされます。 .NET レポートには、プロファイリング対象の型、モジュール、関数、ソース コード行、および命令について、これらのカウントの合計が表示されます。  
  
- ガベージ コレクションが発生すると、プロファイラーは、破棄されたオブジェクトに関するデータと、ガベージ コレクションの各ジェネレーション内のオブジェクトに関する情報を収集します。 プロファイリング実行の終了時には、明示的に破棄されなかったオブジェクトに関するデータが記録されます。 オブジェクトの有効期間レポートには、プロファイリング実行中にメモリが割り当てられた各型の合計が表示されます。  
  
  .NET メモリのプロファイリングは、サンプリング方式またはインストルメンテーション方式で実行できます。 選択するモードによって、.NET メモリのプロファイリングに固有のメモリ割り当てレポートおよびオブジェクトの有効期間レポートに影響が及ぶことはありません。  
  
- .NET メモリのプロファイリングをサンプリング モードで実行すると、サンプリング間隔としてメモリ割り当てイベントが使用され、メモリが割り当てられたオブジェクトの数と、割り当てられたメモリの総バイト数が、レポートの包括値および排他値として表示されます。  
  
- .NET メモリのプロファイリングをインストルメンテーション モードで実行すると、タイミングに関する詳細情報と共に、包括的割り当て値および排他的割り当て値が収集されます。  
  
  [メモリの割り当てとオブジェクトの有効期間のデータ値について](../profiling/understanding-memory-allocation-and-object-lifetime-data-values.md)  
  
  [.NET メモリの割り当ておよび有効期間データの収集](../profiling/collecting-dotnet-memory-allocation-and-lifetime-data.md)  
  
  [.NET メモリデータビュー](../profiling/dotnet-memory-data-views.md)  
  
## <a name="tier-interaction"></a><a name="tier_interaction"></a> 階層の相互作用  
 階層の相互作用のプロファイリングでは、[!INCLUDE[vstecado](../includes/vstecado-md.md)] ページまたはその他のアプリケーションと [!INCLUDE[vstecasp](../includes/vstecasp-md.md)] データベースとの間で行われた同期的な [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 呼び出しに関する情報が、プロファイリング データ ファイルに追加されます。 データには、呼び出しの回数と時間、および最長時間と最短時間が含まれます。 階層の相互作用データは、サンプリング、インストルメンテーション、.NET メモリ、またはコンカレンシーの各方式で収集されたプロファイリング データに追加できます。  
  
 ![階層相互作用プロファイリング データ](../profiling/media/tierinteraction-profilingtools.png "TierInteraction_ProfilingTools")  
プロファイリング ツールによって収集される階層の相互作用データ  
  
 [階層相互作用データの収集](../profiling/collecting-tier-interaction-data.md)  
  
 [階層相互作用のビュー](../profiling/tier-interaction-views.md)  
  
## <a name="see-also"></a>参照  
 [方法: Web サイトのパフォーマンスデータを収集する](../profiling/how-to-collect-performance-data-for-a-web-site.md)   
 [パフォーマンスプロファイルの初心者向けガイド](../profiling/beginners-guide-to-performance-profiling.md)
