---
title: モジュール ビュー - サンプリング データ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Modules view
- sampling profiling method,Modules view
ms.assetid: 816f5633-65d7-41e5-aee1-033628d4e2df
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 5c3aa55bfc521521e28686ebb248053350ae14a7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842073"
---
# <a name="modules-view---sampling-data"></a>モジュール ビュー - サンプリング データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプリング データのモジュール ビューには、プロファイル データでサンプリングされたパフォーマンス データが、モジュールごとにグループ化されて表示されます。 各モジュールが、階層ツリーのルートです。 モジュールのサンプリングされた関数が、モジュール ノードの下に一覧表示されます。  
  
> [!NOTE]
> Windows 8 および Windows Server 2012 の強化されたセキュリティ機能によって、Visual Studio プロファイラーがこれらのプラットフォームでデータを収集する方法に大幅な変更が必要になりました。 Windows ストア アプリにも新しい収集手法が必要です。 ｢[Windows 8 および Windows Server 2012 アプリケーションのパフォーマンス ツール](../profiling/performance-tools-on-windows-8-and-windows-server-2012-applications.md)」を参照してください。  
  
 サンプルの収集時に関数が実行されていた場合 (つまり関数が呼び出し履歴の最上位にあった場合) は、実行されていたソース行および命令アドレスが関数ノードの下に一覧表示されます。 データは行や命令の実行時にソース行または命令ポインターについて収集されるため、行データと命令データの両方の包括値と排他値は常に同じです。  
  
|Column|[説明]|  
|------------|-----------------|  
|**Name**|モジュールの名前、関数、行番号、命令ポインター アドレス。|  
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|  
|**プロセス名**|プロセスの名前です。|  
|**モジュール名**|関数、行、または命令ポインターを含むモジュールの名前。|  
|**モジュール パス**|モジュール、関数、行、または命令ポインターを含むモジュールのパス。|  
|**[転送元ファイル]**|この関数の定義を含むソース ファイルです。|  
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|  
|**包括サンプル数**|-   関数の場合、この関数またはこの関数によって呼び出された関数が実行されたサンプルの数、つまりこの関数を含む呼び出し履歴サンプルの数。<br />-   モジュールの場合、このモジュールの少なくとも 1 つの関数が実行されたサンプルの数。<br />-   行または命令の場合、この行または命令が実行されたサンプルの数。|  
|**サンプル % (子を含む)**|-   関数またはモジュールの場合、プロファイリング実行のすべてのサンプルに対する、関数またはモジュールの包括サンプルの割合。<br />-   行または命令の場合、プロファイリング実行のすべてのサンプルに対する、この行または命令が実行されたサンプルの割合。|  
|**排他サンプル数**|-   関数の場合、この関数が直接実行されていた呼び出し履歴サンプルの数、つまり、この関数が呼び出し履歴の最上位にあったときのサンプルの数。<br />-   モジュールの場合、このモジュール内の関数における排他サンプルの合計。<br />-   行または命令の場合、この行または命令が実行されたサンプルの数。|  
|**排他サンプル %**|-   関数またはモジュールの場合、プロファイリング実行のすべてのサンプルに対する、関数またはモジュールの排他サンプルの割合。<br />-   行または命令の場合、プロファイリング実行のすべてのサンプルに対する、この行または命令が実行されたサンプルの割合。|  
  
## <a name="see-also"></a>参照  
 [モジュールビュー-サンプリング](../profiling/modules-view-dotnet-memory-sampling-data.md)   
 [モジュールビュー-インストルメンテーション](../profiling/modules-view-dotnet-memory-instrumentation-data.md)   
 [[モジュール] ビュー](../profiling/modules-view-instrumentation-data.md)
