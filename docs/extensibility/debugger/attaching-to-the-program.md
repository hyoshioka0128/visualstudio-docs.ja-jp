---
title: プログラムへの添付 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8f39b489a57ab93ba5f2d116738c591bd53ff95f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739240"
---
# <a name="attach-to-the-program"></a>プログラムにアタッチする
適切なポートを使用してプログラムを登録した後、デバッグするプログラムにデバッガをアタッチする必要があります。

## <a name="choose-how-to-attach"></a>アタッチ方法を選択する
 セッション デバッグ マネージャー (SDM) がデバッグ対象のプログラムにアタッチしようとする 3 つの方法があります。

1. デバッグ エンジンによって起動されるプログラムの場合、 [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)メソッド (たとえば、解釈された言語の一般的な) は、アタッチされているプログラムに関連付けられている[IDebugProgramNode2 オブジェクトから IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)インターフェイスを取得します。 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) SDM がインターフェイスを`IDebugProgramNodeAttach2`取得できる場合、SDM は[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出します。 メソッド`IDebugProgramNodeAttach2::OnAttach`は、`S_OK`プログラムにアタッチしなかったこと、およびプログラムにアタッチするために他の試行が行われたことを示すために戻ります。

2. SDM がアタッチ対象のプログラムから[IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)インターフェイスを取得できる場合、SDM は[Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md)メソッドを呼び出します。 このアプローチは、ポートサプライヤーによってリモートで起動されたプログラムに対して一般的です。

3. プログラムを`IDebugProgramNodeAttach2::OnAttach`または`IDebugProgramEx2::Attach`メソッドを介してアタッチできない場合、SDM は`CoCreateInstance`関数を呼び出してデバッグ エンジンを読み込み (まだ読み込まれていない場合)、Attach メソッドを呼び出します。 [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) このアプローチは、ポートサプライヤーによってローカルに起動されるプログラムに典型的です。

    カスタム ポート サプライヤーが、カスタム ポート サプライヤー`IDebugEngine2::Attach`のメソッドの実装でメソッドを`IDebugProgramEx2::Attach`呼び出すこともできます。 通常、この場合、カスタム ポート サプライヤーはリモート コンピューターでデバッグ エンジンを起動します。

   セッション デバッグ マネージャー (SDM) を呼び出すときに接続が[行われます、 Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドです。

   デバッグするアプリケーションと同じプロセスで DE を実行する場合は、[次](../../extensibility/debugger/reference/idebugprogramnode2.md)のメソッドを実装する必要があります。

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  メソッドが`IDebugEngine2::Attach`呼び出された後、メソッドの実装で次の`IDebugEngine2::Attach`手順を実行します。

1. [イベント](../../extensibility/debugger/reference/idebugenginecreateevent2.md)オブジェクトを SDM に送信します。 詳細については、[イベントの送信](../../extensibility/debugger/sending-events.md)を参照してください。

2. メソッドに渡された[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトの[GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)メソッド`IDebugEngine2::Attach`を呼び出します。

     プログラムを識別`GUID`するために使用される を返します。 ローカル`GUID`プログラムを表すオブジェクトに DE を格納する必要があり、`IDebugProgram2::GetProgramId``IDebugProgram2`メソッドがインターフェイスで呼び出されたときに返す必要があります。

    > [!NOTE]
    > インターフェイスを実装すると`IDebugProgramNodeAttach2`、プログラムはメソッドに`GUID``IDebugProgramNodeAttach2::OnAttach`渡されます。 これは`GUID`、メソッドによって`GUID`返されるプログラムに使用されます`IDebugProgram2::GetProgramId`。

3. イベント[オブジェクトを送信](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)して、プログラムを DE に表すためにローカル`IDebugProgram2`オブジェクトが作成されたことを SDM に通知します。 詳細については、[イベントの送信](../../extensibility/debugger/sending-events.md)を参照してください。

    > [!NOTE]
    > これは、`IDebugEngine2::Attach`メソッドに渡`IDebugProgram2`されたオブジェクトと同じではありません。 渡された`IDebugProgram2`オブジェクトはポートでのみ認識され、独立したオブジェクトです。

## <a name="see-also"></a>関連項目
- [起動ベースの添付ファイル](../../extensibility/debugger/launch-based-attachment.md)
- [イベントの送信](../../extensibility/debugger/sending-events.md)
- [LaunchSuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)
- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)
- [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)
- [IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)
- [OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)
- [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)
- [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)
- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)
- [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)
