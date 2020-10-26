---
title: '方法: マネージド コードのスレッド名を設定する | Microsoft Docs'
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
- Thread.Name property
- threading [Visual Studio], names
- thread names
- debugging [Visual Studio], threads
ms.assetid: c0c4d74a-0314-4b71-81c9-b0b019347ab8
caps.latest.revision: 31
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: b800fbd2f39d75f110a059c70b87a203eb72e7d6
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68157673"
---
# <a name="how-to-set-a-thread-name-in-managed-code"></a>方法: マネージド コードのスレッド名を設定する
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

スレッド名の設定は、Visual Studio のどのエディションでも実行できます。 スレッド名を設定すると、 **[スレッド]** ウィンドウでスレッドを追跡する際に役立ちます。 Visual Studio Express のエディションでは [ **スレッド** ] ウィンドウを使用できないため、Express edition ではスレッドの名前付けにほとんどユーティリティがありません。  
  
 マネージド コードのスレッド名を設定するには、<xref:System.Threading.Thread.Name%2A> プロパティを使用します。  
  
## <a name="example"></a>例  
  
```  
Public Class Needle  
    ' This method will be called when the thread is started.  
    Sub Baz()  
        Console.WriteLine("Needle Baz is running on another thread")  
    End Sub  
End Class  
  
Sub Main()  
    Console.WriteLine("Thread Simple Sample")  
    Dim oNeedle As New Needle()  
   ' Create a Thread object.   
    Dim oThread As New System.Threading.Thread(AddressOf oNeedle.Baz)  
    ' Set the Thread name to "MainThread".  
    oThread.Name = "MainThread"  
    ' Starting the thread invokes the ThreadStart delegate  
    oThread.Start()  
End Sub  
```  
  
## <a name="see-also"></a>参照  
 [マルチスレッドアプリケーションのデバッグ](../debugger/debug-multithreaded-applications-in-visual-studio.md)   
 [方法: ネイティブ コードのスレッド名を設定する](../debugger/how-to-set-a-thread-name-in-native-code.md)
