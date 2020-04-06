---
title: デバッガを起動する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- debugging [Debugging SDK], launching the debugger
- debugger [Debugging SDK], launching
ms.assetid: f24da1a1-f923-48b4-989f-18a22b581d1b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ceb2f484449d1b3f8474a6586d298b057875b342
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738449"
---
# <a name="launch-the-debugger"></a>デバッガを起動する
デバッガを起動するには、適切な属性を使用して、正しい一連のメソッドとイベントを送信する必要があります。

## <a name="sequences-of-methods-and-events"></a>メソッドとイベントのシーケンス

1. セッション デバッグ マネージャー (SDM) は、[**デバッグ**] メニューを選択し、[**開始**] をクリックして呼び出されます。 詳細については、「[プログラムの起動」を](../../extensibility/debugger/launching-a-program.md)参照してください。

2. SDM は[OnAttach](../../extensibility/debugger/reference/idebugprogramnodeattach2-onattach.md)メソッドを呼び出します。

3. デバッグ エンジン (DE) プロセス モデルに`IDebugProgramNodeAttach2::OnAttach`基づいて、メソッドは次のメソッドのいずれかを返し、次に何が起こるかを決定します。

     戻`S_FALSE`り値が返された場合、デバッグ エンジン (DE) は仮想マシンのプロセスで読み込まれます。

     \- または -

     戻`S_OK`り値が返された場合、DE は SDM のインプロセスでロードされます。 SDM は次のタスクを実行します。

    1. 呼び出しは、DE のエンジン情報を取得するのには[、 GetEngineInfo](../../extensibility/debugger/reference/idebugprogramnode2-getengineinfo.md)です。

    2. DE を共同作成します。

    3. 呼び出し[アタッチ](../../extensibility/debugger/reference/idebugengine2-attach.md)。

4. デは、属性を持つ SDM に[IDebugEngineCreateEvent2](../../extensibility/debugger/reference/idebugenginecreateevent2.md)を送信します`EVENT_SYNC`。

5. デは、属性を持つ SDM に[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)を送信します`EVENT_SYNC`。

6. デは、属性を持つ SDM に[IDebugThreadCreateEvent2](../../extensibility/debugger/reference/idebugthreadcreateevent2.md)を送信します`EVENT_SYNC`。

7. デは、属性を持つ SDM に[IDebugLoadCompleteEvent2](../../extensibility/debugger/reference/idebugloadcompleteevent2.md)を送信します`EVENT_SYNC`。

8. 属性を持つ SDM に[IDebugEntryPointEvent2](../../extensibility/debugger/reference/idebugentrypointevent2.md)を送信します`EVENT_SYNC`。

## <a name="see-also"></a>関連項目
- [デバッガ イベントの呼び出し](../../extensibility/debugger/calling-debugger-events.md)
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
