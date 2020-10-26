---
title: レポート用のフック関数 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.hooks
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- hooks, report
- _CrtDbgReport function
- debugger, report hook functions
- memory allocation, debug heap
- debugging [C++], hook functions
- _CrtSetReportHook function
- report hook functions
ms.assetid: 1854bca7-d7eb-4502-89bf-b1ee64cb50ef
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 0a492a1db8b65cad74d02cec0f43bf0c81461730
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65687508"
---
# <a name="report-hook-functions"></a>レポート用のフック関数
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

[_CrtSetReportHook](https://msdn.microsoft.com/library/1ae7c64f-8c84-4797-9574-b59f00f7a509) を使用してインストールされたレポート用のフック関数は、[_CrtDbgReport](https://msdn.microsoft.com/library/6e581fb6-f7fb-4716-9432-f0145d639ecc) がデバッグ レポートを生成するたびに呼び出されます。 レポート用のフック関数を使用して、特定の割り当て型に関するレポートだけを出力できます。 レポート用のフック関数には、次のようなプロトタイプが必要です。  
  
```  
int YourReportHook(int nRptType, char *szMsg, int *retVal);  
```  
  
 **_CrtSetReportHook** に渡すポインターは **_CRT_REPORT_HOOK** 型です。これらは CRTDBG.H に次のように定義されています。  
  
```  
typedef int (__cdecl *_CRT_REPORT_HOOK)(int, char *, int *);  
```  
  
 ランタイム ライブラリが独自のフック関数を呼び出す場合は、引数 *nRptType* には、レポートのカテゴリ ( **_CRT_WARN**、 **_CRT_ERROR**、または **_CRT_ASSERT**) が含まれます。引数 *szMsg* には、レポート用の完全にアセンブルされたメッセージ文字列へのポインターが含まれます。また、*retVal* には、`_CrtDbgReport` がレポート作成後に通常どおり実行を継続するのか、デバッガーを起動するのかを示す値が含まれます。 (*retVal* の値が 0 の場合は実行を継続し、1 の場合はデバッガーを起動します。)  
  
 フック関数でメッセージを完全に処理できたため、それ以上レポートを出力する必要がない場合は、**TRUE** を返すようにします。 **FALSE** を返した場合は、`_CrtDbgReport` は通常どおりにレポート メッセージを出力します。  
  
## <a name="see-also"></a>参照  
 [デバッグ用フック関数の作成](../debugger/debug-hook-function-writing.md)   
 [crt_dbg2 のサンプル](https://msdn.microsoft.com/21e1346a-6a17-4f57-b275-c76813089167)
