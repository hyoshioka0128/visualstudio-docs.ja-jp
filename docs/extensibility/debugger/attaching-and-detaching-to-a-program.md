---
title: プログラムへのアタッチとデタッチ |Microsoft Docs
description: デバッガーをアタッチするための適切な属性を使用して、メソッドとイベントの正しいシーケンスを送信する方法について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
- debug engines, detaching from programs
ms.assetid: 79dcbb9b-c7f8-40fc-8a00-f37fe1934f51
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6b71a78dcee62f89dee4c54b53c1026f42895793
ms.sourcegitcommit: 8e9c38da7bcfbe9a461c378083846714933a0e1e
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 12/09/2020
ms.locfileid: "96913790"
---
# <a name="attaching-and-detaching-to-a-program"></a>プログラムへのアタッチとデタッチ
デバッガーをアタッチするには、適切な属性を持つメソッドとイベントの正しいシーケンスを送信する必要があります。

## <a name="sequence-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッションデバッグマネージャー (SDM) は、 [Onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。

    デバッグエンジン (DE) プロセスモデルに基づいて、 `IDebugProgramNodeAttach2::OnAttach` メソッドは次のいずれかのメソッドを返します。これにより次の処理が決定されます。

    が返された場合は、 `S_FALSE` デバッグエンジンがプログラムに正常にアタッチされています。 それ以外の場合は、 [attach メソッドを呼び出してアタッチ](../../extensibility/debugger/reference/idebugengine2-attach.md) プロセスを完了します。

    が返された場合 `S_OK` 、DE は SDM と同じプロセスに読み込まれます。 SDM は、次のタスクを実行します。

   1. [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)を呼び出して、DE のエンジン情報を取得します。

   2. DE を共同作成します。

   3. [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)を呼び出します。

2. DE は、属性を使用して [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。

3. DE は、属性を使用して [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。

4. DE は、属性を使用して [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) を SDM に送信し `EVENT_SYNC_STOP` ます。

   プログラムからのデタッチは、次のように、簡単な2段階のプロセスです。

5. SDM は [デタッチ](../../extensibility/debugger/reference/idebugprogram2-detach.md)を呼び出します。

6. DE は [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)を送信します。

## <a name="see-also"></a>関連項目
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
