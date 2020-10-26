---
title: '方法: OnStart メソッドをデバッグする | Microsoft Docs'
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
- OnStart method
- debugging [Visual Studio], Windows services
- debugging managed code, OnStart method
- debugging Windows Services applications, OnStart method
- Windows Service applications, debugging
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
caps.latest.revision: 19
author: MikeJo5000
ms.author: mikejo
manager: jillfra
ms.openlocfilehash: 391b906889dcbe422f7ec227b1d375be82e7ac91
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "65700172"
---
# <a name="how-to-debug-the-onstart-method"></a>方法: OnStart メソッドをデバッグする
[!INCLUDE[vs2017banner](../includes/vs2017banner.md)]

Windows サービスをデバッグするには、サービスを起動し、デバッガーをサービス プロセスにアタッチします。 詳細については、「[方法:Windows サービス アプリケーションをデバッグする](https://msdn.microsoft.com/library/63ab0800-0f05-4f1e-88e6-94c73fd920a2) ただし、Windows サービスの <xref:System.ServiceProcess.ServiceBase.OnStart%2A?displayProperty=fullName> メソッドをデバッグするには、メソッド内部からデバッガーを起動する必要があります。  
  
1. <xref:System.Diagnostics.Debugger.Launch%2A> メソッドの始めに、呼び出しを `OnStart()`に追加します。  
  
    ```csharp  
    protected override void OnStart(string[] args)  
    {  
        System.Diagnostics.Debugger.Launch();  
     }  
    ```  
  
2. サービスを開始します ( `net start`を使うか、 **[サービス]** ウィンドウで開始することができます)。  
  
     次のようなダイアログ ボックスが表示されます。  
  
     ![OnStartDebug](../debugger/media/onstartdebug.png "OnStartDebug")  
  
3. **[はい、\<service name> をデバッグします]** をクリックします。  
  
4. [Just-In-Time デバッガー] ウィンドウで、デバッグに使う Visual Studio のバージョンを選びます。  
  
     ![JustInTimeDebugger](../debugger/media/justintimedebugger.png "JustInTimeDebugger")  
  
5. Visual Studio の新しいインスタンスが開始し、 `Debugger.Launch()` メソッドで実行が停止します。  
  
## <a name="see-also"></a>参照  
 [デバッガーのセキュリティ](../debugger/debugger-security.md)   
 [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
