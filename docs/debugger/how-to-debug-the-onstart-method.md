---
title: '方法: OnStart メソッドをデバッグする | Microsoft Docs'
ms.date: 11/04/2016
ms.topic: conceptual
dev_langs:
- CSharp
- VB
- FSharp
- C++
helpviewer_keywords:
- OnStart method
- debugging [Visual Studio], Windows services
- debugging managed code, OnStart method
- debugging Windows Services applications, OnStart method
- Windows Service applications, debugging
ms.assetid: b06b5d65-424b-490f-bf58-97583cd7006a
author: mikejo5000
ms.author: mikejo
manager: jillfra
ms.workload:
- multiple
ms.openlocfilehash: 107ce6d5ca2b327d77fe588e1ac7ffda10a0a3a3
ms.sourcegitcommit: 5f6ad1cefbcd3d531ce587ad30e684684f4c4d44
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 10/22/2019
ms.locfileid: "72733621"
---
# <a name="how-to-debug-the-onstart-method"></a>方法: OnStart メソッドをデバッグする
Windows サービスをデバッグするには、サービスを起動し、デバッガーをサービス プロセスにアタッチします。 詳細については、[Windows サービス アプリケーションをデバッグする](/dotnet/framework/windows-services/how-to-debug-windows-service-applications) ただし、Windows サービスの <xref:System.ServiceProcess.ServiceBase.OnStart%2A?displayProperty=fullName> メソッドをデバッグするには、メソッド内部からデバッガーを起動する必要があります。

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

3. **[はい、** service name> をデバッグします]\< を選びます。

4. [Just-In-Time デバッガー] ウィンドウで、デバッグに使う Visual Studio のバージョンを選びます。

    ![JustInTimeDebugger](../debugger/media/justintimedebugger.png "JustInTimeDebugger")

5. Visual Studio の新しいインスタンスが開始し、 `Debugger.Launch()` メソッドで実行が停止します。

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
