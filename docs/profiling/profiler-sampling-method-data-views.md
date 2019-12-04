---
title: プロファイラー サンプリング メソッドのデータ ビュー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- Profiling Tools,sampling data views
- sampling data views
ms.assetid: 798de693-e43a-4056-aff5-48310c2172c5
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: 8d845d84d421ca44f5b936df0a7138fefa848d8d
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74772163"
---
# <a name="profiler-sampling-method-data-views"></a>プロファイラー サンプリング メソッドのデータ ビュー
ここでは、サンプリング メソッドを使用して生成されたプロファイラー データ ファイルのビューとレポートに関するリファレンス情報を示します。

> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 UWP アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。

## <a name="in-this-section"></a>このセクションの内容
- [概要 ビュー](../profiling/summary-view-sampling-data.md)

 サンプルの収集時に最も頻繁に実行された関数、および最も多くの個別作業を実行した関数が一覧表示されます。

- [コール ツリー ビュー](../profiling/call-tree-view-sampling-data.md)

 関数の実行パスが階層ツリーで表示されます。

- [モジュール ビュー](../profiling/modules-view-sampling-data.md)

 プロファイル データがモジュールごとに整理され、サンプルの収集時に実行された関数、ソース コードの行、および命令が一覧表示されます。

- [呼び出し元/呼び出し先ビュー - サンプリング データ](../profiling/caller-callee-view-sampling-data.md)

 選択した関数と、選択した関数を呼び出した関数および選択した関数によって呼び出された関数のプロファイル データが表示されます。

- [関数ビュー](../profiling/functions-view-sampling-data.md)

 プロファイリングが関数ごとに整理され、サンプルの収集時に実行された関数が一覧表示されます。

- [行ビュー](../profiling/lines-view-sampling-data.md)

 サンプルの収集時に実行されたソース コード行が一覧表示されます。

- [命令ポインター (IP) ビュー](../profiling/instruction-pointers-ips-view-sampling-data.md)

 サンプルの収集時に実行されたソース コード行が一覧表示されます。

## <a name="reference"></a>辞書／辞典／その他
- [プロセス ビュー](../profiling/process-view.md)

 プロセスおよびスレッドの開始時刻と終了時刻が一覧表示されます。

- [マーク ビュー](../profiling/marks-view.md)

 プロファイル データ ファイルに挿入された ETW およびサンプリング イベントが一覧表示されます。

- [関数の詳細ビュー](../profiling/function-details-view.md)

 選択した関数と、選択した関数を呼び出した関数および選択した関数によって呼び出された関数の関係がグラフィカルな図で表示されます。

## <a name="related-sections"></a>関連項目
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)

 インストルメンテーション メソッドを使用して生成されたプロファイラー データ ファイルのビューとレポートに関するリファレンス情報。

- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)

 .NET メモリ データを含むプロファイラー データ ファイルのビューとレポートに関するリファレンス情報。

## <a name="see-also"></a>関連項目
- [サンプリング データ値について](../profiling/understanding-sampling-data-values.md)
