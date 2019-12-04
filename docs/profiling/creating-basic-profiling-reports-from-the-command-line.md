---
title: コマンド ラインからの基本的なプロファイリング レポートの作成 | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
ms.assetid: 6d73e21e-c04e-48ea-91cc-e517a5f2cd3f
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: cd9748d88a9398792274c386a42bdaa3ce48ba70
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74777791"
---
# <a name="create-basic-profiling-reports-from-the-command-line"></a>コマンド ラインから基本的なプロファイリング レポートを作成する
この記事では、.*vsp* プロファイル データ ファイルまたは .*vsps* プロファイル データ ファイルからコンマ区切り値 (.*csv*) レポートを生成する基本的な VSPerfReport コマンドについて説明します。 すべてのレポート オプションの詳細については、「[VSPerfReport](../profiling/vsperfreport.md)」を参照してください。

## <a name="report-commands"></a>レポート コマンド
 指定したプロファイル データ ファイルのレポートを作成するには、次のいずれかのコマンドを使用します。

 **VSPerfReport** `VSPFile` **/Summary:All** *.vsp* ファイルまたは *.vsps* ファイルで利用できるすべてのレポートが生成されます。

 **VSPerfReport** `VSPFile` **/Summary:** `ReportType`[,`ReportType`...] 指定した種類のレポートが生成されます。

 **VSPerfReport** `VSPFile` **/CallTrace** 各データ コレクション イベントが一覧表示されたレポートが生成されます。 インストルメンテーションでのみ使用します。

## <a name="summary-report-type-parameters"></a>概要レポートの型パラメーター
 レポートの種類オプションの指定によって生成されるレポートの説明を次の表に示します。 レポートに表示される列は、データの収集に使用されたプロファイル方法によって異なります。

|概要パラメーター|レポートの説明|レポートの参考情報|
|-----------------------|------------------------|----------------------|
|**CallerCallee**|関数間の親子関係が表示されます。|-   [サンプリング データ](../profiling/caller-callee-view-sampling-data.md)<br />-   [インストルメンテーション データ](../profiling/caller-callee-view-instrumentation-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/caller-callee-view-dotnet-memory-sampling-data.md)<br />-   [.NET メモリ インストルメンテーション データ](../profiling/caller-callee-view-net-memory-instrumentation-data.md)<br />-   [競合データ](../profiling/caller-callee-view-contention-data.md)|
|**Function**|プロファイル データが関数別に一覧表示されます。|-   [サンプリング データ](../profiling/functions-view-sampling-data.md)<br />-   [インストルメンテーション データ](../profiling/functions-view-instrumentation-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/functions-view-dotnet-memory-sampling-data.md)<br />-   [.NET メモリ インストルメンテーション データ](../profiling/functions-view-dotnet-memory-instrumentation-data.md)<br />-   [競合データ](../profiling/functions-view-contention-data.md)|
|**CallTree**|プロファイリング実行の実行パスおよび関数のプロファイル データが表示されます。|-   [インストルメンテーション データ](../profiling/call-tree-view-instrumentation-data.md)<br />-   [サンプリング データ](../profiling/call-tree-view-sampling-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/call-tree-view-dotnet-memory-sampling-data.md)<br />-   [.NET メモリ インストルメンテーション データ](../profiling/call-tree-view-dotnet-memory-instrumentation-data.md)<br />-   [競合データ](../profiling/call-tree-view-contention-data.md)|
|**カウンター**|プロファイリング実行中に収集されたプロファイル マークおよび Windows パフォーマンス カウンター値が一覧表示されます。|-   [マーク ビュー](../profiling/marks-view.md)|
|**Ip**|プロファイル データが命令別に一覧表示されます。|-   [サンプリング データ](../profiling/instruction-pointers-ips-view-sampling-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/instruction-pointers-ips-view-dotnet-memory-sampling-data.md)<br />-   [競合データ](../profiling/instruction-pointers-ips-view-contention-data.md)|
|**Life**|割り当てられたオブジェクトの有効期間が一覧表示されます。|-   [オブジェクトの有効期間ビュー](../profiling/object-lifetime-view.md)|
|**Line**|プロファイル データがソース コード行別に一覧表示されます。|-   [サンプリング データ](../profiling/lines-view-sampling-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/lines-view-dotnet-memory-sampling-data.md)<br />-   [競合データ](../profiling/lines-view-contention-data.md)|
|**Header**|プロファイル データ ファイルのヘッダー情報です。|ファイルによって異なります。|
|**マーク**|プロファイル実行中に収集されたプロファイル マークが表示されます。|-   [マーク ビュー](../profiling/marks-view.md)|
|**Module**|モジュールのプロファイル データが一覧表示されます。|-   [サンプリング データ](../profiling/modules-view-sampling-data.md)<br />-   [インストルメンテーション データ](../profiling/modules-view-instrumentation-data.md)<br />-   [.NET メモリ サンプリング データ](../profiling/modules-view-dotnet-memory-sampling-data.md)<br />-   [.NET メモリ インストルメンテーション データ](../profiling/modules-view-dotnet-memory-instrumentation-data.md)<br />-   [競合データ](../profiling/modules-view-contention-data.md)|
|**Process**|プロセスのプロファイル データが一覧表示されます。|-   [プロセス ビュー](../profiling/process-view.md)<br />-   [競合データ](../profiling/process-view-contention-data.md)|
|**スレッド**|スレッドのプロファイル データが一覧表示されます。|-   [プロセス ビュー](../profiling/process-view.md)|
|**Type**|割り当てプロファイル データが種類別に一覧表示されます。|-   [割り当て ビュー](../profiling/dotnet-memory-allocations-view.md)|
|**Contention**|リソースの競合が表示されます。|-   [リソースの競合](../profiling/resource-contentions-view-contention-data.md)|
|**RuleWarnings**|パフォーマンス規則の問題が一覧表示されます。|-   規則の問題の CheckId、説明、およびソース コードの場所が一覧表示されます。|
|**ETW**|プロファイリング実行で収集された ETW (Event Tracing for Windows) イベントが一覧表示されます。|-   [ETW レポート](../profiling/event-tracing-for-windows-etw-report.md)|
