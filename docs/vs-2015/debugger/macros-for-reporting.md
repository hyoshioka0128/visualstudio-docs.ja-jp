---
title: レポート用マクロ | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.macros
dev_langs:
- FSharp
- VB
- CSharp
- C++
- C++
helpviewer_keywords:
- macros, CRT reporting macros
- macros, debugging with
- _RPTFn macro
- CRT, reporting macros
- debugging [CRT], reporting macros
- _RPTn macro
ms.assetid: f2085314-a3a8-4caf-a5a4-2af9ad5aad05
caps.latest.revision: 18
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: e4aee33d571f95e24a359fa2bc7e12ae8d64eae0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62431629"
---
# <a name="macros-for-reporting"></a>レポート用マクロの使用
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

CRTDBG.H で定義されている **_RPTn**と **_RPTFn** マクロを使用できます。H。デバッグ用のステートメントの使用を置き換え `printf` ます。 これらのマクロは **_DEBUG** が定義されていない場合にリリースビルドで自動的に消去されるため、 **#ifdef**s で囲む必要はありません。  
  
|マクロ|説明|  
|-----------|-----------------|  
|**_RPT0**、 **_RPT1**、 **_RPT2**、 **_RPT3**、 **_RPT4**|メッセージ文字列と、0 から 4 個の引数を出力します。 _RPT1 から **_RPT4** の場合、メッセージ文字列は、引数に対して printf 形式の書式設定文字列として機能します。|  
|**_RPTF0**、 **_RPTF1**、、 **_RPTF2**、 **_RPTF4**|**_RPTn**と同じですが、マクロが配置されているファイル名と行番号も出力されます。|  
  
 次に例を示します。  
  
```  
#ifdef _DEBUG  
    if ( someVar > MAX_SOMEVAR )  
        printf( "OVERFLOW! In NameOfThisFunc( ),  
               someVar=%d, otherVar=%d.\n",  
               someVar, otherVar );  
#endif  
```  
  
 このコードは、`someVar` の値と `otherVar` の値を **stdout** に出力します。 次のように `_RPTF2` を呼び出すと、これらの値と一緒にファイル名と行番号も出力できます。  
  
```  
if (someVar > MAX_SOMEVAR) _RPTF2(_CRT_WARN, "In NameOfThisFunc( ), someVar= %d, otherVar= %d\n", someVar, otherVar );  
```  
  
 特定のアプリケーションでは、C ランタイム ライブラリのマクロで提供されているデバッグ レポートでは不十分な場合があります。その場合は、独自の要件を満たす専用のマクロを設計できます。 たとえば、ヘッダー ファイルの 1 つに、次のような **ALERT_IF2** というマクロを定義するコードを含めることができます。  
  
```  
#ifndef _DEBUG                  /* For RELEASE builds */  
#define  ALERT_IF2(expr, msg, arg1, arg2)  do {} while (0)  
#else                           /* For DEBUG builds   */  
#define  ALERT_IF2(expr, msg, arg1, arg2) \  
    do { \  
        if ((expr) && \  
            (1 == _CrtDbgReport(_CRT_ERROR, \  
                __FILE__, __LINE__, msg, arg1, arg2))) \  
            _CrtDbgBreak( ); \  
    } while (0)  
#endif  
```  
  
 このトピックの冒頭で、 **ALERT_IF2** の1回の呼び出しで、 **printf** コードのすべての関数を実行できます。  
  
```  
ALERT_IF2(someVar > MAX_SOMEVAR, "OVERFLOW! In NameOfThisFunc( ),   
someVar=%d, otherVar=%d.\n", someVar, otherVar );  
```  
  
 カスタム マクロは、目的に応じて出力情報の量を増減したり、出力先を変更したりなどの変更を簡単に実現できるため、デバッグ要件が複雑さを増してくる段階で使用すると便利です。  
  
## <a name="see-also"></a>参照  
 [CRT のデバッグ技術](../debugger/crt-debugging-techniques.md)
