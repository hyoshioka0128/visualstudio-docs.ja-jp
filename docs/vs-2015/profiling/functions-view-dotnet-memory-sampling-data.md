---
title: 関数ビュー - .NET メモリ サンプリング データ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
helpviewer_keywords:
- Functions view
ms.assetid: 5d9c6302-2ffd-430e-9535-13ce795f9f7c
caps.latest.revision: 14
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 8e77c6c2b3bf079e8aae88c9779c3b487ff97fe7
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68141868"
---
# <a name="functions-view---net-memory-sampling-data"></a>関数ビュー - .NET メモリ サンプリング データ
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

サンプリング メソッドを使用して収集された .NET メモリの割り当てプロファイル データの関数ビューには、プロファイル実行中にメモリを割り当てた関数が一覧表示され、割り当てのサイズと数が報告されます。  
  
|Column|[説明]|  
|------------|-----------------|  
|**プロセス ID**|プロファイリング実行のプロセス ID (PID) です。|  
|**プロセス名**|プロセスの名前です。|  
|**モジュール名**|関数を含むモジュールの名前です。|  
|**モジュール パス**|関数を含むモジュールのパスです。|  
|**[転送元ファイル]**|この関数の定義を含むソース ファイルです。|  
|**関数名**|関数の完全修飾名です。|  
|**関数行番号**|ソース ファイルでのこの関数の開始行番号です。|  
|**関数アドレス**|関数のアドレス。|  
|**割り当て数 (子を含む)**|この関数とその子関数で割り当てられたオブジェクトの総数。|  
|**割り当て % (子を含む)**|プロファイル実行で割り当てられたすべてのオブジェクトに対する、この関数の包括的割り当てであったオブジェクトの割合。|  
|**割り当て数 (関数のみ)**|その関数が呼び出し履歴の最上位で直接実行されたときに作成されたオブジェクトの数。 この数には、子関数で作成されたオブジェクトが含まれません。|  
|**割り当て % (関数のみ)**|プロファイル実行で割り当てられたすべてのオブジェクトに対する、この関数の排他的割り当てであったオブジェクトの割合。|  
|**割り当てバイト数 (子を含む)**|この関数とその子関数で割り当てられたメモリのバイト数。|  
|**割り当てバイト数 % (子を含む)**|プロファイル実行で割り当てられたすべてのメモリのバイト数に対する、この関数の包括バイトであったバイト数の割合。|  
|**割り当てバイト数 (関数のみ)**|この関数によって割り当てられたメモリのバイト数。その子関数によるものは含まれません。|  
|**割り当てバイト数 % (関数のみ)**|プロファイル実行で割り当てられたすべてのメモリのバイト数に対する、この関数の排他バイトであったバイト数の割合。|  
  
## <a name="see-also"></a>参照  
 [関数ビュー-インストルメンテーション](../profiling/functions-view-dotnet-memory-instrumentation-data.md)   
 [関数ビュー](../profiling/functions-view-sampling-data.md)   
 [関数 ビュー](../profiling/functions-view-instrumentation-data.md)
