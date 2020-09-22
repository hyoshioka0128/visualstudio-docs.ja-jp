---
title: 関数ビュー - サンプリング データ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- sampling profiling method,Functions View
- Functions view
ms.assetid: 029d5ebb-e551-46b0-b64e-2c553d9dbb8e
caps.latest.revision: 17
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5aace03631cd768566dca8e314f280e20d9de77f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90841836"
---
# <a name="functions-view---sampling-data"></a>関数ビュー - サンプリング データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプリング プロファイル方式の関数のレポート ビューには、プロファイリング実行中にサンプリングされた関数が一覧表示されます。  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 「[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
|Column|説明|  
|------------|-----------------|  
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|  
|**プロセス名**|プロセスの名前です。|  
|**モジュール名**|関数を含むモジュールの名前です。|  
|**モジュール パス**|関数を含むモジュールのパスです。|  
|**ソース ファイル**|この関数の定義を含むソース ファイルです。|  
|**関数名**|関数の完全修飾名です。|  
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|  
|**関数アドレス**|関数のアドレス。|  
|**サンプル数 (子を含む)**|この関数が実行されたときに収集されたサンプルの合計数。つまり、この関数が呼び出し履歴上にあったときに収集されたサンプルの数。 この数には、その関数によって呼び出された関数の実行中に収集されたサンプルが含まれます。|  
|**包括サンプル %**|プロファイル実行のすべてのサンプルに対する、この関数の包括サンプルの割合。|  
|**サンプル数 (関数のみ)**|この関数の本文内のコードが実行されたとき、つまり、この関数が呼び出し履歴の一番上にあったときに収集されたサンプルの合計数。 この関数によって呼び出された関数で収集されたサンプルは含まれません。|  
|**サンプル % (関数のみ)**|プロファイル実行のすべてのサンプルに対する、この関数の排他サンプルの割合。|  
  
## <a name="see-also"></a>参照  
 [方法: レポートビューの列をカスタマイズする](../profiling/how-to-customize-report-view-columns.md)   
 [関数ビュー-インストルメンテーション](../profiling/functions-view-dotnet-memory-instrumentation-data.md)   
 [関数ビュー-サンプリング](../profiling/functions-view-dotnet-memory-sampling-data.md)   
 [関数ビュー](../profiling/functions-view-instrumentation-data.md)
