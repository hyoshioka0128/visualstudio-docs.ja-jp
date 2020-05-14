---
title: 起動後のアタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 3a4ce0a7465891035b43bbb8f6f22f0c064d104c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739282"
---
# <a name="attach-after-a-launch"></a>起動後にアタッチする
プログラムが起動すると、デバッグ セッションは、デバッグ エンジン (DE) をそのプログラムにアタッチする準備が整います。

## <a name="design-decisions"></a>設計上の決定
 共有アドレス空間内での通信は簡単であるため、デバッグ セッションと DE 間の通信を設定する 2 つの設計方法を選択する必要があります。 または、DE とプログラム間の通信を設定します。 次のいずれかを選択します。

- デバッグ セッションと DE 間の通信を設定する方が意味がある場合、デバッグ セッションは DE を共同作成し、DE にプログラムへのアタッチを要求します。 この設計では、デバッグ セッションと DE は 1 つのアドレス空間に一緒に残され、ランタイム環境とプログラムは別のアドレス空間に一緒に残されます。

- DE とプログラム間の通信をセットアップする方が意味がある場合は、実行時環境が DE を同時に作成します。 この設計では、SDM が 1 つのアドレス空間に残され、DE、ランタイム環境、およびプログラムが別のアドレス空間に残されます。 この設計は、スクリプト言語を実行するインタープリターで実装される DE の典型的な設計です。

    > [!NOTE]
    > DE がプログラムにアタッチする方法は、実装に依存します。 DE とプログラム間の通信も実装に依存します。

## <a name="implementation"></a>実装
 プログラムを使用して、セッション デバッグ マネージャー (SDM) が最初に起動するプログラムを表す[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトを受け取ると[、Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md)メソッドを呼び出し、後でデバッグ イベントを SDM に渡すために使用される[IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)オブジェクトを渡します。 メソッド`IDebugProgram2::Attach`は[、次に OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出します。 SDM が`IDebugProgram2`インターフェイスを受信する方法の詳細については、[ポートへの通知を](../../extensibility/debugger/notifying-the-port.md)参照してください。

 デは、デバッグしているプログラムと同じアドレス空間で実行する必要がある場合: DEは、通常、スクリプトを実行しているインタープリターの一部であるため、`IDebugProgramNodeAttach2::OnAttach`メソッドは`S_FALSE`返します。 戻`S_FALSE`り値は、アタッチプロセスが完了したことを示します。

 ただし、DE が SDM のアドレス空間で実行される場合:`IDebugProgramNodeAttach2::OnAttach`メソッド`S_OK`が返すか[、IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)インターフェイスがデバッグ中のプログラムに関連付けられた[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトにまったく実装されていません。 この場合、アタッチ操作を完了するために[、Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドが呼び出されます。

 後者の場合は、`IDebugEngine2::Attach`メソッドに渡`GUID`された`GUID``IDebugProgram2::GetProgramId``IDebugProgram2`オブジェクトに対して[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)メソッドを呼び出し、 ローカル プログラム オブジェクトに格納し、このオブジェクトでメソッドが呼び出されたときにこれを返す必要があります。 `GUID`は、さまざまなデバッグ コンポーネント間でプログラムを一意に識別するために使用されます。

 メソッドが`IDebugProgramNodeAttach2::OnAttach`返される`S_FALSE`場合は、プログラムに`GUID`使用する メソッドが、ローカル プログラム オブジェクト`IDebugProgramNodeAttach2::OnAttach``GUID`に対してを設定するメソッドに渡されます。

 これで、DE がプログラムにアタッチされ、スタートアップ イベントを送信する準備が整いました。

## <a name="see-also"></a>関連項目
- [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
