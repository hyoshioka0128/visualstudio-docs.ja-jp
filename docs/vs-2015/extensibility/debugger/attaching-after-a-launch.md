---
title: 起動後のアタッチ |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 5a3600a1-dc20-4e55-b2a4-809736a6ae65
caps.latest.revision: 15
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 693cf6d746f51862415f2f30e46d48a998047f14
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "90842266"
---
# <a name="attaching-after-a-launch"></a>起動後のアタッチ
[!INCLUDE[vs2017banner](../../includes/vs2017banner.md)]

プログラムが起動した後、デバッグセッションはデバッグエンジン (DE) をプログラムにアタッチする準備ができています。  
  
## <a name="design-decisions"></a>設計上の決定事項  
 共有アドレス空間内での通信が容易になるため、デバッグセッションと DE の間、または DE とプログラムの間の通信を容易にするために、より有意義な方法であるかどうかを判断する必要があります。 次のいずれかを選択します。  
  
- デバッグセッションと DE との間の通信を容易にするために、デバッグセッションは de を併置し、プログラムへのアタッチを解除するように要求します。 これにより、デバッグセッションと重複除去が1つのアドレス空間に残り、実行時の環境とプログラムが互いにまとめられます。  
  
- DE とプログラムの間の通信を容易にするために、実行時環境によって重複除去が実行されます。 これにより、SDM は1つのアドレス空間に残り、逆に、実行時環境、およびプログラムは相互にまとめられます。 これは、スクリプト化された言語を実行するインタープリターで実装される DE の一般的なものです。  
  
    > [!NOTE]
    > プログラムへの DE のアタッチは、実装に依存します。 また、DE とプログラムの間の通信も実装に依存します。  
  
## <a name="implementation"></a>実装  
 プログラムによって、セッションデバッグマネージャー (SDM) は、最初に起動するプログラムを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) オブジェクトを受け取るときに、 [Attach](../../extensibility/debugger/reference/idebugprogram2-attach.md) メソッドを呼び出し、 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) オブジェクトを渡します。これは、後でデバッグイベントを SDM に渡すために使用されます。 次に、 `IDebugProgram2::Attach` メソッドは [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。 SDM がインターフェイスを受信する方法の詳細につい `IDebugProgram2` ては、「 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)」を参照してください。  
  
 デバッグ中のプログラムと同じアドレス空間で DE を実行する必要がある場合、通常はスクリプトを実行しているインタープリターの一部であるため、 `IDebugProgramNodeAttach2::OnAttach` このメソッドはを返し `S_FALSE` ます。これは、アタッチプロセスが完了したことを示します。  
  
 一方、SDM のアドレス空間で DE が実行されている場合、 `IDebugProgramNodeAttach2::OnAttach` メソッドはを返し `S_OK` ます。または、 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md) インターフェイスが、デバッグ中のプログラムに関連付けられている [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) オブジェクトのまったく実装されていません。 この場合、 [attach メソッドが呼び出されて、](../../extensibility/debugger/reference/idebugengine2-attach.md) アタッチ操作が完了します。  
  
 後者の場合は、メソッドに渡されたオブジェクトで [Getprogramid](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md) メソッド `IDebugProgram2` `IDebugEngine2::Attach` を呼び出し、 `GUID` ローカルプログラムオブジェクトにを格納して、この `GUID` `IDebugProgram2::GetProgramId` オブジェクトでメソッドが呼び出されたときにこれを返す必要があります。 は、 `GUID` さまざまなデバッグコンポーネントに対してプログラムを一意に識別するために使用されます。  
  
 メソッドがを `IDebugProgramNodeAttach2::OnAttach` 返す場合 `S_FALSE` 、 `GUID` プログラムに使用するは、そのメソッドに渡され、 `IDebugProgramNodeAttach2::OnAttach` ローカルプログラムオブジェクトでを設定するメソッドになることに注意して `GUID` ください。  
  
 これで、DE がプログラムにアタッチされ、スタートアップイベントを送信する準備が整いました。  
  
## <a name="see-also"></a>参照  
 [プログラムに直接アタッチする](../../extensibility/debugger/attaching-directly-to-a-program.md)   
 [ポートへの通知](../../extensibility/debugger/notifying-the-port.md)   
 [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)   
 [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md)   
 [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)   
 [外付け](../../extensibility/debugger/reference/idebugprogram2-attach.md)   
 [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)   
 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)   
 [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)   
 [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)   
 [[アタッチ]](../../extensibility/debugger/reference/idebugengine2-attach.md)
