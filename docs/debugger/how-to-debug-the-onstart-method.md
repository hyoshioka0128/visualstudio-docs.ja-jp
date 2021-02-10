---
title: OnStart メソッドをデバッグする | Microsoft Docs
description: メソッド内からデバッガーを起動して、Visual Studio で Windows サービスの OnStart メソッドをデバッグする方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
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
manager: jmartens
ms.workload:
- multiple
ms.openlocfilehash: 51096d7a47de80be7434659936165ba0a29f7c67
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99899284"
---
# <a name="how-to-debug-the-onstart-method"></a>方法: OnStart メソッドをデバッグする
Windows サービスをデバッグするには、サービスを起動し、デバッガーをサービス プロセスにアタッチします。 詳細については、「[方法:Windows サービス アプリケーションをデバッグする](/dotnet/framework/windows-services/how-to-debug-windows-service-applications) ただし、Windows サービスの <xref:System.ServiceProcess.ServiceBase.OnStart%2A?displayProperty=fullName> メソッドをデバッグするには、メソッド内部からデバッガーを起動する必要があります。

1. <xref:System.Diagnostics.Debugger.Launch%2A> メソッドの始めに、呼び出しを `OnStart()`に追加します。

    ```csharp
    protected override void OnStart(string[] args)
    {
        System.Diagnostics.Debugger.Launch();
    }
    ```

2. サービスを開始します ( `net start`を使うか、 **[サービス]** ウィンドウで開始することができます)。

    次のようなダイアログ ボックスが表示されます。

    ![WindowsService-Asis.exe で発生した未処理の .NET Framework 例外を示す Visual Studio の [Just-In-Time デバッガー] ダイアログ ボックスのスクリーンショット。](../debugger/media/onstartdebug.png)

3. **[はい、\<service name> をデバッグします]** をクリックします。

4. [Just-In-Time デバッガー] ウィンドウで、デバッグに使う Visual Studio のバージョンを選びます。

    ![使用可能なデバッガーの一覧で "Microsoft Visual Studio 2015 の新しいインスタンス" が選択されている、Visual Studio の [Just-In-Time デバッガー] ウィンドウのスクリーンショット。](../debugger/media/justintimedebugger.png)

5. Visual Studio の新しいインスタンスが開始し、 `Debugger.Launch()` メソッドで実行が停止します。

## <a name="see-also"></a>関連項目
- [デバッガーのセキュリティ](../debugger/debugger-security.md)
- [マネージド コードをデバッグする](../debugger/debugging-managed-code.md)
