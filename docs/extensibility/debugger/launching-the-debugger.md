---
title: デバッガーを起動しています |Microsoft Docs
description: メソッドとイベントのシーケンスと、デバッガーを起動するために必要な適切な属性について説明します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b9f8bc85672fc89205ab25fa9954e1c28e10f859
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926385"
---
# <a name="launch-the-debugger"></a>デバッガーを起動します
デバッガーを起動するには、適切な属性を使用してメソッドとイベントの正しいシーケンスを送信する必要があります。

## <a name="sequences-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッションデバッグマネージャー (SDM) を呼び出すには、[ **デバッグ** ] メニューを選択し、[ **開始**] をクリックします。 詳細については、「 [プログラムの起動](../../extensibility/debugger/launching-a-program.md)」を参照してください。

2. SDM は [Onattach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md) メソッドを呼び出します。

3. デバッグエンジン (DE) プロセスモデルに基づいて、 `IDebugProgramNodeAttach2::OnAttach` メソッドは次のいずれかのメソッドを返します。これにより次の処理が決定されます。

     が `S_FALSE` を返した場合、デバッグエンジン (DE) は仮想マシンのプロセスで読み込まれます。

     \- または -

     が `S_OK` を返した場合、DE は SDM のインプロセスで読み込まれます。 その後、SDM は次のタスクを実行します。

    1. [GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)を呼び出して、DE のエンジン情報を取得します。

    2. DE を共同作成します。

    3. [Attach](../../extensibility/debugger/reference/idebugengine2-attach.md)を呼び出します。

4. DE は、属性を使用して [IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。

5. DE は、属性を使用して [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。

6. DE は、属性を使用して [IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md) を SDM に送信し `EVENT_SYNC` ます。

7. DE は、属性を使用して [IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md) を SDM に送信し `EVENT_SYNC` ます。

8. DE は、属性を使用して [IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md) を SDM に送信し `EVENT_SYNC` ます。

## <a name="see-also"></a>関連項目
- [呼び出し (デバッガーイベントを)](../../extensibility/debugger/calling-debugger-events.md)
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
