---
title: プログラムへのアタッチとデタッチ |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d8bd6ea4b51c56a3cc42036b7bd26d34ff3a3eff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80739267"
---
# <a name="attaching-and-detaching-to-a-program"></a>プログラムへのアタッチとデタッチ
デバッガをアタッチするには、適切な属性を使用してメソッドとイベントの正しいシーケンスを送信する必要があります。

## <a name="sequence-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッション デバッグ マネージャー (SDM) は[、OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出します。

    デバッグ エンジン (DE) プロセス モデルに`IDebugProgramNodeAttach2::OnAttach`基づいて、メソッドは次のメソッドのいずれかを返し、次に何が起こるかを決定します。

    返`S_FALSE`された場合、デバッグ エンジンはプログラムに正常にアタッチされています。 それ以外の場合は[、Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)メソッドが呼び出され、アタッチプロセスが完了します。

    戻`S_OK`された場合、DE は SDM と同じプロセスにロードされます。 SDM は、次のタスクを実行します。

   1. 呼び出しは、DE のエンジン情報を取得するのには[、 GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)です。

   2. DE を共同作成します。

   3. 呼び出し[アタッチ](../../extensibility/debugger/reference/idebugengine2-attach.md)。

2. デは、属性を持つ SDM に[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)を送信します`EVENT_SYNC`。

3. デは、属性を持つ SDM に[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)を送信します`EVENT_SYNC`。

4. デは、属性を持つ SDM に[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)を送信します`EVENT_SYNC_STOP`。

   プログラムからのデタッチは、次の 2 段階の単純なプロセスです。

5. SDM は[デタッチ](../../extensibility/debugger/reference/idebugprogram2-detach.md)を呼び出します。

6. デは[、IDebug プログラムデストロイイベント2 を](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)送信します。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
