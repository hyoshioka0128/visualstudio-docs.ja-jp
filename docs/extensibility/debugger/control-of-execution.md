---
title: 実行制御 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], control of execution
ms.assetid: 97071846-007e-450f-95a6-f072d0f5e61e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: e2d338c5470611a5eea0c6279404c4eaddebb2d0
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739078"
---
# <a name="control-of-execution"></a>実行の制御
デバッグ エンジン (DE) は、通常、最後のスタートアップ イベントとして次のいずれかのイベントを送信します。

- 新しく起動したプログラムにアタッチする場合は、エントリ ポイント イベント

- 既に実行中のプログラムにアタッチする場合は、ロード完了イベント

  これらのイベントはどちらもイベントを停止しています。 詳細については、[操作モード](../../extensibility/debugger/operational-modes.md)を参照してください。

## <a name="stopping-event"></a>停止イベント
 停止イベントがデバッグセッションに送信されると、次のようになります。

1. 現在の命令ポインターを含むプログラムとスレッドは、イベント・インターフェースから取得できます。

2. IDE は、エディタで強調表示された状態で表示される現在のソース コード ファイルと位置を決定します。

3. デバッグ セッションは通常、プログラムの**Continue**メソッドを呼び出すことによって、この最初の停止イベントに応答します。

4. その後、ブレークポイントを押すなどの停止状態が発生するまで、プログラムが実行されます。 この場合、DE はブレークポイント イベントをデバッグ セッションに送信します。 ブレークポイント イベントは停止イベントであり、DE はユーザーの応答を再度待機します。

5. ユーザーが関数にステップ インするか、関数を上にするか、または関数からステップ アウトするか選択した場合、IDE は`Step`デバッグ セッションにプログラムのメソッドを呼び出すように求めるプロンプトを出します。 IDE は、ステップの単位 (命令、ステートメント、または行) とステップの種類 (ステップイン、オーバー、または関数から除外するかどうか) を渡します。 ステップが完了すると、DE はステップ完了イベントをデバッグ・セッション (停止イベント) に送信します。

    \- または -

    ユーザーが現在の命令ポインターから実行を続行することを選択した場合、IDE は、プログラムの**Execute**メソッドを呼び出すようにデバッグ セッションを要求します。 プログラムは、次の停止条件に遭遇するまで実行を再開します。

    \- または -

    デバッグ セッションが特定の停止イベントを無視する場合、デバッグ セッションはプログラムの**Continue**メソッドを呼び出します。 停止状態が発生したときに、プログラムが関数にステップ イン、オーバー、またはアウトを実行した場合、そのプログラムはステップを続行します。

   プログラムを使用して、DE が停止状態を検出すると[、IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)インターフェイスを使用して、セッション デバッグ マネージャー (SDM) に[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)または[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)などの停止イベントを送信します。 DE は、プログラムと現在の命令ポインターを含むスレッドを表す[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)および[IDebugThread2](../../extensibility/debugger/reference/idebugthread2.md)インターフェイスを渡します。 SDM は、一番上のスタック フレームを取得するために[IDebugThread2::EnumFrameInfo](../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)を呼び出し、現在の命令ポインターに関連付けられているドキュメント コンテキストを取得するために[IDebugStackFrame2::GetDocumentContext](../../extensibility/debugger/reference/idebugstackframe2-getdocumentcontext.md)を呼び出します。 このドキュメント コンテキストは、通常、ソース コード ファイル名、行、および列番号です。 IDE では、これらのコードを使用して、現在の命令ポインターを含むソース コードを強調表示します。

   SDM は通常、この最初の停止イベントに対して[IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)を呼び出して応答します。 その後、ブレークポイントを押すなどの停止状態が発生するまでプログラムが実行され、その場合、DE は[IDebugBreakpointEvent2 インターフェイス](../../extensibility/debugger/reference/idebugbreakpointevent2.md)を SDM に送信します。 ブレークポイント イベントは停止イベントであり、DE はユーザーの応答を再度待機します。

   ユーザーが関数にステップ インするか、関数を上にするか、または関数からステップ アウトするか選択した場合、IDE は SDM に対して[IDebugProgram2::Step](../../extensibility/debugger/reference/idebugprogram2-step.md)を呼び出すように求めます。 その後、IDE は[STEPUNIT](../../extensibility/debugger/reference/stepunit.md) (命令、ステートメント、または行) と[STEPKIND](../../extensibility/debugger/reference/stepkind.md)を渡します。 手順が完了すると、DE は停止イベントである SDM に[IDebugStepCompleteEvent2](../../extensibility/debugger/reference/idebugstepcompleteevent2.md)インターフェイスを送信します。

   ユーザーが現在の命令ポインターから実行を続行することを選択した場合、IDE は SDM に[IDebugProgram2::Execute](../../extensibility/debugger/reference/idebugprogram2-execute.md)を呼び出すかどうかを要求します。 プログラムは、次の停止条件に遭遇するまで実行を再開します。

   デバッグ パッケージが特定の停止イベントを無視する場合、デバッグ パッケージは[、IDebugProgram2::Continue](../../extensibility/debugger/reference/idebugprogram2-continue.md)を呼び出す SDM を呼び出します。 停止状態が発生したときに、プログラムが関数にステップ イン、オーバー、またはアウトを実行していた場合、そのプログラムはステップを続行します。 これは、プログラムがステップ実行状態を維持し、続行する方法を認識していることを意味します。

   SDM**が、** 実行`Step`、および**Continue**に対して行う呼び出しは非同期であり、SDM は呼び出しがすぐに戻ることを期待します。 DE が、SDM を停止イベントを送信してから`Step`、**実行**、または**続行**が戻ると、SDM はハングします。

## <a name="see-also"></a>関連項目
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
