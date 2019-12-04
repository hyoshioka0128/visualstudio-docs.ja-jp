---
title: プロセス ビュー | Microsoft Docs
ms.date: 11/04/2016
ms.topic: conceptual
f1_keywords:
- vs.performance.view.process
helpviewer_keywords:
- performance tools reports, process view
- Process view
- performance tools, process view
- Profiling Tools,process view
- Profiling Tools,process report
ms.assetid: 6d4e2a5d-9f17-4ece-a6f1-75836e1fc382
author: mikejo5000
ms.author: mikejo
manager: jillfra
monikerRange: vs-2017
ms.workload:
- multiple
ms.openlocfilehash: da3097c276557238e6f5b521f6f7d3231434cd10
ms.sourcegitcommit: 00b71889bd72b6a566586885bdb982cfe807cf54
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/03/2019
ms.locfileid: "74772177"
---
# <a name="process-view"></a>プロセス ビュー
プロセス ビューには、プロファイリング実行中に実行されたプロセスとスレッドのプロファイル データが表示されます。

 プロセスは、名前ごとに一覧表示されます。 スレッドは、そのスレッドを作成したプロセスの子ノードとして一覧表示されます。 スレッドには、ストレージを開始した関数の名前、または使用できるシンボルがない場合はラベルの名前 **[ntdll.dll]** が付けられます。

 列を追加または削除するには、ビューを右クリックし、 **[列の追加と作業時間]** を選択します。 また、データを並べ替えるには、列名をクリックします。 詳細については、[レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)」を参照してください。

 プロセス ビューの列は、サンプリング メソッドとインストルメンテーション メソッドで生成されたデータ、および .NET メモリ データを含むデータの列と同じです。 次の表に列の値を示します。

|Column|説明|
|------------|-----------------|
|**ID (一意)**|プロファイラーによって生成される、プロセスまたはスレッドに固有の ID。|
|**ID**|システムによって生成される、プロセスまたはスレッドの ID。|
|**Name**|プロセスまたはスレッドの名前。|
|**開始時刻**|プロファイリングの開始からプロセスまたはスレッドの開始までの時間 (ミリ秒) またはプロセッサ サイクル数。|
|**終了時刻**|プロファイリングの開始からプロセスまたはスレッドの終了までの時間 (ミリ秒) またはプロセッサ サイクル数。|

## <a name="see-also"></a>関連項目
- [サンプリング メソッドのデータ ビュー](../profiling/profiler-sampling-method-data-views.md)
- [インストルメンテーション メソッドのデータ ビュー](../profiling/instrumentation-method-data-views.md)
- [.NET メモリのデータ ビュー](../profiling/dotnet-memory-data-views.md)
