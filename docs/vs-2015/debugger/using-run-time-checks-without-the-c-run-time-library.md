---
title: C ランタイム ライブラリなしのランタイム チェックの使用方法 | Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
f1_keywords:
- vs.debug.runtime
dev_langs:
- FSharp
- VB
- CSharp
- C++
- JScript
- VB
- CSharp
- C++
helpviewer_keywords:
- run-time errors, error checks
- CRT, run-time checks
- debugger, native run-time checks
- run-time errors, run-time checks
- run-time checks, /RTC option
- debugging [Visual Studio], run-time routines
ms.assetid: 30ed90f3-9323-4784-80a4-937449eb54f6
caps.latest.revision: 20
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 1eefddd21817360736b9f20f74ca3dc8a83683fe
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65684020"
---
# <a name="using-run-time-checks-without-the-c-run-time-library"></a>C ランタイム ライブラリなしのランタイム チェックの使用方法
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

**/NODEFAULTLIB** を使用して C ランタイム ライブラリなしでプログラムをリンクしているときに、ランタイム チェックを使用する場合は、RunTmChk.lib とリンクする必要があります。  
  
 `_RTC_Initialize` は、ランタイム チェックでプログラムを初期化します。 C ランタイム ライブラリとリンクしない場合は、次のように、プログラムが `_RTC_Initialize` を呼び出す前に、ランタイム エラー チェックでコンパイルされているかどうかを確認する必要があります。  
  
```  
#ifdef __MSVC_RUNTIME_CHECKS  
    _RTC_Initialize();  
#endif  
```  
  
 C ランタイム ライブラリをリンクしない場合は、`_CRT_RTC_INITW` と呼ばれる関数も定義する必要があります。 `_CRT_RTC_INITW` は、次に示すように、ユーザー定義関数を既定のエラー レポート関数としてインストールします。  
  
```  
// C version:  
_RTC_error_fnW __cdecl _CRT_RTC_INITW(  
        void *res0, void **res1, int res2, int res3, int res4)  
{  
    // set the error handler.  
    return &MyErrorFunc;   
}  
  
// C++ version:  
extern "C" _RTC_error_fnW __cdecl _CRT_RTC_INITW(  
       void *res0, void **res1, int res2, int res3, int res4)  
{  
    // set the error handler:  
    return &MyErrorFunc;  
}  
```  
  
 既定のエラー レポート関数を組み込むと、`_RTC_SetErrorFuncW` を使用して追加のエラー レポート関数を組み込むことができます。 詳細については、「[_RTC_SetErrorFuncW](https://msdn.microsoft.com/library/b3e0d71f-1bd3-4c37-9ede-2f638eb3c81a)」を参照してください。  
  
## <a name="see-also"></a>参照  
 [方法: ネイティブ ランタイム チェックを使用する](../debugger/how-to-use-native-run-time-checks.md)
