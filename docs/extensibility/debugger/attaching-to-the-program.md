---
title: プログラムへのアタッチ |Microsoft Docs
description: プログラムが適切なポートに登録された後に、Visual Studio がプログラムにアタッチするデバッガーを実装する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: 9a3f5b83-60b5-4ef0-91fe-a432105bd066
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 030ee19e7e9e9e52140fb41da78f766978e18d3f
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96913764"
---
# <a name="attach-to-the-program"></a>プログラムにアタッチする
プログラムを適切なポートに登録したら、デバッグ対象のプログラムにデバッガーをアタッチする必要があります。

## <a name="choose-how-to-attach"></a>アタッチ方法の選択
 セッションデバッグマネージャー (SDM) がデバッグ中のプログラムへのアタッチを試行するには、3つの方法があります。

1. [Launchsuspended](../../extensibility/debugger/reference/idebugenginelaunch2-launchsuspended.md)メソッド (解釈された言語など) を通じてデバッグエンジンによって起動されるプログラムの場合、SDM は、アタッチされているプログラムに関連付けられている[IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)オブジェクトから[IDebugProgramNodeAttach2](../../extensibility/debugger/reference/idebugprogramnodeattach2.md)インターフェイスを取得します。 SDM がインターフェイスを取得できる場合 `IDebugProgramNodeAttach2` 、sdm は [onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。 `IDebugProgramNodeAttach2::OnAttach`メソッドは、 `S_OK` プログラムにアタッチされていないこと、および他の試行をプログラムにアタッチできることを示すためにを返します。

2. SDM がアタッチされているプログラムから [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md) インターフェイスを取得できる場合、Sdm は [Attach](../../extensibility/debugger/reference/idebugprogramex2-attach.md) メソッドを呼び出します。 この方法は、ポートサプライヤーによってリモートで起動されたプログラムには一般的です。

3. またはメソッドを使用してプログラムをアタッチできない場合 `IDebugProgramNodeAttach2::OnAttach` `IDebugProgramEx2::Attach` 、SDM は関数を呼び出してデバッグエンジン (まだ読み込まれていない場合) を読み込み、 `CoCreateInstance` その後 [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを呼び出します。 この方法は、ポートサプライヤーによってローカルに起動されるプログラムには一般的です。

    カスタムポート供給業者が `IDebugEngine2::Attach` メソッドのカスタムポートサプライヤーの実装でメソッドを呼び出すこともでき `IDebugProgramEx2::Attach` ます。 通常、この場合、カスタムポートサプライヤーは、リモートコンピューターでデバッグエンジンを起動します。

   添付ファイルは、セッションデバッグマネージャー (SDM) が [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md) メソッドを呼び出すと実行されます。

   デバッグ対象のアプリケーションと同じプロセスで DE を実行する場合は、 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md)の次のメソッドを実装する必要があります。

- [GetHostName](../../extensibility/debugger/reference/idebugprogramnode2-gethostname.md)

- [GetHostPid](../../extensibility/debugger/reference/idebugprogramnode2-gethostpid.md)

- [GetProgramName](../../extensibility/debugger/reference/idebugprogramnode2-getprogramname.md)

  `IDebugEngine2::Attach`メソッドが呼び出された後、メソッドの実装で次の手順を実行し `IDebugEngine2::Attach` ます。

1. [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)イベントオブジェクトを SDM に送信します。 詳細については、「 [イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

2. メソッドに渡された[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)オブジェクトに対して[getprogramid](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)メソッドを呼び出し `IDebugEngine2::Attach` ます。

     これは、 `GUID` プログラムを識別するために使用されるを返します。 は、 `GUID` ローカルプログラムを表すオブジェクトに、DE に格納されている必要があります。また、 `IDebugProgram2::GetProgramId` インターフェイスでメソッドが呼び出されたときに返される必要があり `IDebugProgram2` ます。

    > [!NOTE]
    > インターフェイスを実装すると `IDebugProgramNodeAttach2` 、プログラムの `GUID` がメソッドに渡され `IDebugProgramNodeAttach2::OnAttach` ます。 これ `GUID` は `GUID` 、メソッドによって返されるプログラムのために使用され `IDebugProgram2::GetProgramId` ます。

3. [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントオブジェクトを送信して、プログラムを表すためにローカルオブジェクトが作成されたことを SDM に通知し `IDebugProgram2` ます。 詳細については、「 [イベントの送信](../../extensibility/debugger/sending-events.md)」を参照してください。

    > [!NOTE]
    > これは `IDebugProgram2` 、メソッドに渡されたオブジェクトと同じではありません `IDebugEngine2::Attach` 。 以前に渡されたオブジェクトは、 `IDebugProgram2` ポートでのみ認識され、独立したオブジェクトです。

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
- [[アタッチ]](../../extensibility/debugger/reference/idebugprogramex2-attach.md)
- [[アタッチ]](../../extensibility/debugger/reference/idebugengine2-attach.md)
