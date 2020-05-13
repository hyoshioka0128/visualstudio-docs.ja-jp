---
title: 例外処理マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], exception handling
ms.assetid: 7279dc16-db14-482c-86b8-7b3da5a581d2
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 34b83c7181a7ba405e642d9911e2c53df3f4401d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738764"
---
# <a name="exception-handling-visual-studio-sdk"></a>例外処理
例外がスローされたときに発生するプロセスを次に示します。

## <a name="exception-handling-process"></a>例外処理プロセス

1. 例外が最初にスローされたが、デバッグ中のプログラムの例外ハンドラーによって処理される前に、デバッグ エンジン (DE) は、停止イベントとしてセッション デバッグ マネージャー (SDM) に[IDebugExceptionEvent2](../../extensibility/debugger/reference/idebugexceptionevent2.md)を送信します。 `IDebugExceptionEvent2`例外の設定 (デバッグ パッケージの [例外] ダイアログ ボックスで指定) のみが、ユーザーが初回例外通知で停止することを指定した場合に送信されます。

2. SDM は、例外のプロパティを取得するために[IDebugExceptionEvent2 を呼び](../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)出します。

3. デバッグ パッケージは、ユーザーに提示するオプションを決定するために[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)を呼び出します。

4. デバッグ パッケージは、初回例外ダイアログ ボックスを開いて例外を処理する方法をユーザーに確認します。

5. ユーザーが続行することを選択した場合、SDM は[IDebugExceptionEvent2 を](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)呼び出します。

    - メソッドがS_OKを返す場合は[、IDebugExceptionEvent2::PassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)を呼び出します。

         \- または -

         メソッドがS_FALSEを返す場合、デバッグ中のプログラムは例外を処理する 2 度目の機会を与えられます。

6. デバッグ中のプログラムに 2 度目の例外のハンドラーがない場合、DE は SDM`IDebugExceptionEvent2`に**EVENT_SYNC_STOP**として を送信します。

7. デバッグ パッケージは、初回例外ダイアログ ボックスを開いて例外を処理する方法をユーザーに確認します。

8. デバッグ パッケージは、ユーザーに提示するオプションを決定するために[IDebugExceptionEvent2::CanPassToDebuggee](../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)を呼び出します。

9. デバッグ パッケージは、2 番目のエラーの例外ダイアログ ボックスを開くことによって、例外を処理する方法をユーザーに確認します。

10. メソッドがS_OKを返す場合`IDebugExceptionEvent2::PassToDebuggee`は、 を呼び出します。

## <a name="see-also"></a>関連項目
- [デバッガー イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
