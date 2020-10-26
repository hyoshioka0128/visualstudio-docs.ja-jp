---
title: プロセス ビュー | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
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
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0436401c458a7d6771a2785028a8b5fe0ef57546
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180221"
---
# <a name="process-view"></a>プロセス ビュー
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プロセス ビューには、プロファイリング実行中に実行されたプロセスとスレッドのプロファイル データが表示されます。  
  
 プロセスは、名前ごとに一覧表示されます。 スレッドは、そのスレッドを作成したプロセスの子ノードとして一覧表示されます。 スレッドには、ストレージを開始した関数の名前、または使用できるシンボルがない場合はラベルの名前 **[ntdll.dll]** が付けられます。  
  
 列を追加または削除するには、ビューを右クリックし、 **[列の追加と作業時間]** を選択します。 また、データを並べ替えるには、列名をクリックします。 詳細については、「[方法: レポート ビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)」を参照してください。  
  
 プロセス ビューの列は、サンプリング メソッドとインストルメンテーション メソッドで生成されたデータ、および .NET メモリ データを含むデータの列と同じです。 次の表に列の値を示します。  
  
|Column|[説明]|  
|------------|-----------------|  
|**ID (一意)**|プロファイラーによって生成される、プロセスまたはスレッドに固有の ID。|  
|**ID**|システムによって生成される、プロセスまたはスレッドの ID。|  
|**Name**|プロセスまたはスレッドの名前。|  
|**開始時刻**|プロファイリングの開始からプロセスまたはスレッドの開始までの時間 (ミリ秒) またはプロセッサ サイクル数。|  
|**[終了時刻]**|プロファイリングの開始からプロセスまたはスレッドの終了までの時間 (ミリ秒) またはプロセッサ サイクル数。|  
  
## <a name="see-also"></a>参照  
 [サンプリングメソッドのデータビュー](../profiling/profiler-sampling-method-data-views.md)   
 [インストルメンテーションメソッドのデータビュー](../profiling/instrumentation-method-data-views.md)   
 [.NET メモリデータビュー](../profiling/dotnet-memory-data-views.md)
