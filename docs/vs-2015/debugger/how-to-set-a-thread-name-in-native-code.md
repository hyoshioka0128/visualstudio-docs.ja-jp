---
title: '方法: ネイティブ コードのスレッド名を設定する | Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-debug
ms.topic: conceptual
dev_langs:
- FSharp
- VB
- CSharp
- C++
helpviewer_keywords:
- debugging [C++], threads
- SetThreadName function
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c85d0968-9f22-4d69-87f4-acca2ae777b8
caps.latest.revision: 40
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 37554c8ba72257ee78b219774425c7e8acb305a2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68156672"
---
# <a name="how-to-set-a-thread-name-in-native-code"></a>方法: ネイティブ コードのスレッド名を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

プログラムにスレッド名を設定するには、次のコード例のように、 `SetThreadName` 関数を使用します。 スレッド名はスレッドにコピーされるため、 `threadName` パラメーターのメモリは解放できます。  
  
## <a name="example"></a>例  
  
```cpp  
//  
// Usage: SetThreadName ((DWORD)-1, "MainThread");  
//  
#include <windows.h>  
const DWORD MS_VC_EXCEPTION = 0x406D1388;  
#pragma pack(push,8)  
typedef struct tagTHREADNAME_INFO  
{  
    DWORD dwType; // Must be 0x1000.  
    LPCSTR szName; // Pointer to name (in user addr space).  
    DWORD dwThreadID; // Thread ID (-1=caller thread).  
    DWORD dwFlags; // Reserved for future use, must be zero.  
 } THREADNAME_INFO;  
#pragma pack(pop)  
void SetThreadName(DWORD dwThreadID, const char* threadName) {  
    THREADNAME_INFO info;  
    info.dwType = 0x1000;  
    info.szName = threadName;  
    info.dwThreadID = dwThreadID;  
    info.dwFlags = 0;  
#pragma warning(push)  
#pragma warning(disable: 6320 6322)  
    __try{  
        RaiseException(MS_VC_EXCEPTION, 0, sizeof(info) / sizeof(ULONG_PTR), (ULONG_PTR*)&info);  
    }  
    __except (EXCEPTION_EXECUTE_HANDLER){  
    }  
#pragma warning(pop)  
}  
  
```  
  
## <a name="see-also"></a>参照  
 [マルチスレッドアプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [デバッガーでのデータの表示](../debugger/viewing-data-in-the-debugger.md)   
 [方法: マネージド コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-managed-code.md)
