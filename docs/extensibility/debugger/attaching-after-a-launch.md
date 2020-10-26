---
title: 起動後のアタッチ |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80739282"
---
# <a name="attach-after-a-launch"></a>起動後にアタッチする
プログラムが起動した後、デバッグセッションはデバッグエンジン (DE) をプログラムにアタッチする準備ができています。

## <a name="design-decisions"></a>設計上の決定
 通信は共有アドレス空間内で簡単に行うことができるため、2つのデザイン方法を選択する必要があります。デバッグセッションと DE の間の通信を設定する方法です。 または、DE とプログラムの間の通信を設定します。 次のいずれかを選択します。

- デバッグセッションと DE との間の通信を設定する方が合理的な場合は、デバッグセッションによって DE が作成され、プログラムへのアタッチを解除するように求められます。 この設計では、1つのアドレス空間、および実行時の環境とプログラムを別のアドレス空間にまとめて、デバッグセッションと逆の組み合わせを作成します。

- DE とプログラムの間の通信を設定する方が合理的な場合は、実行時環境によって DE が作成されます。 この設計では、SDM を1つのアドレス空間に残し、逆に、実行時環境、およびプログラムを別のアドレス空間にまとめます。 この設計は、スクリプト化された言語を実行するインタープリターで実装される DE の一般的なものです。

    > [!NOTE]
    > プログラムへの DE のアタッチは、実装に依存します。 また、DE とプログラムの間の通信も実装に依存します。

## <a name="implementation"></a>実装
 プログラムによって、セッションデバッグマネージャー (SDM) は、最初に起動するプログラムを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトを受け取るときに、 [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) メソッドを呼び出し、 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクトを渡します。これは、後でデバッグイベントを SDM に渡すために使用されます。 次に、 `IDebugProgram2::Attach` メソッドは [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。 SDM がインターフェイスを受信する方法の詳細につい `IDebugProgram2` ては、「 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)」を参照してください。

 デバッグ中のプログラムと同じアドレス空間で DE を実行する必要がある場合: DE は通常、スクリプトを実行しているインタープリターの一部であるため、 `IDebugProgramNodeAttach2::OnAttach` メソッドはを返し `S_FALSE` ます。 `S_FALSE`戻り値は、アタッチプロセスが完了したことを示します。

 ただし、DE が SDM のアドレス空間で実行される場合、メソッドは `IDebugProgramNodeAttach2::OnAttach` を返します。 `S_OK` または、 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスが、デバッグ中のプログラムに関連付けられている [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトに実装されていません。 この場合、 [attach メソッドが呼び出されて、](../../extensibility/debugger/reference/idebugengine2-attach.md) アタッチ操作が完了します。

 後者の場合は、メソッドに渡されたオブジェクトで [Getprogramid](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) メソッド `IDebugProgram2` `IDebugEngine2::Attach` を呼び出し、 `GUID` ローカルプログラムオブジェクトにを格納して、この `GUID` `IDebugProgram2::GetProgramId` オブジェクトでメソッドが呼び出されたときにこれを返す必要があります。 は、 `GUID` さまざまなデバッグコンポーネントに対してプログラムを一意に識別するために使用されます。

 メソッドがを返す場合 `IDebugProgramNodeAttach2::OnAttach` `S_FALSE` 、 `GUID` プログラムに使用するは、そのメソッドに渡されます。これは、 `IDebugProgramNodeAttach2::OnAttach` `GUID` ローカルプログラムオブジェクトでを設定するメソッドです。

 これで、DE がプログラムにアタッチされ、スタートアップイベントを送信する準備が整いました。

## <a name="see-also"></a>関連項目
- [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)
- [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
- [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugprogram2-attach.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugengine2-attach.md)
