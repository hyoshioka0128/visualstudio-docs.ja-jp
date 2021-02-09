---
title: 例外処理 (Visual Studio SDK) |Microsoft Docs
description: 例外がスローされたときに発生するプロセスについて説明します。 この記事では、関連するすべての手順について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ed8db28a7196551e2f1c8236d71e0f2291fce934
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99921514"
---
# <a name="exception-handling-visual-studio-sdk"></a>例外処理 (Visual Studio SDK)
次に、例外がスローされた場合に発生する処理について説明します。

## <a name="exception-handling-process"></a>例外処理プロセス

1. 例外が最初にスローされたときに、デバッグ中のプログラムの例外ハンドラーによって処理される前に、デバッグエンジン (DE) は [IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md) をセッションデバッグマネージャー (SDM) に停止イベントとして送信します。 は、 `IDebugExceptionEvent2` 例外の設定 (デバッグパッケージの [例外] ダイアログボックスで指定したもの) のみを使用して、ユーザーが初回例外通知を停止することを指定した場合に送信されます。

2. SDM は [IDebugExceptionEvent2:: GetException](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md) を呼び出して、例外のプロパティを取得します。

3. デバッグパッケージは、 [IDebugExceptionEvent2:: Can Stoデバッグ](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) を呼び出して、ユーザーに提示するオプションを決定します。

4. デバッグパッケージは、初回例外のダイアログボックスを開いて、例外を処理する方法をユーザーに要求します。

5. ユーザーが続行を選択した場合、SDM は [IDebugExceptionEvent2:: Can Stoデバッグ](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)を呼び出します。

    - メソッドが S_OK を返す場合、は [IDebugExceptionEvent2::P assToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)を呼び出します。

         \- または -

         メソッドが S_FALSE を返すと、デバッグ中のプログラムには、例外を処理するための2つ目の機会が与えられます。

6. デバッグ中のプログラムに2つ目の例外のハンドラーがない場合、DE は `IDebugExceptionEvent2` **EVENT_SYNC_STOP** として SDM にを送信します。

7. デバッグパッケージは、初回例外のダイアログボックスを開いて、例外を処理する方法をユーザーに要求します。

8. デバッグパッケージは、 [IDebugExceptionEvent2:: Can Stoデバッグ](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md) を呼び出して、ユーザーに提示するオプションを決定します。

9. デバッグパッケージは、2回目の例外ダイアログボックスを開いて、例外を処理する方法をユーザーに要求します。

10. メソッドが S_OK を返す場合、はを呼び出し `IDebugExceptionEvent2::PassToDebuggee` ます。

## <a name="see-also"></a>関連項目
- [デバッガーイベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
