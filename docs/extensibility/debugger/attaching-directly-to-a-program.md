---
title: プログラムに直接アタッチする |Microsoft Docs
ms.date: 11/04/2016
ms.topic: how-to
helpviewer_keywords:
- debug engines, attaching to programs
ms.assetid: ad2b7db8-821c-440c-ba07-c55c6a395e0f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dc78234b31b98865f1779dd65d743d4196f9cbf5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "85903270"
---
# <a name="attach-directly-to-a-program"></a>プログラムに直接アタッチする
既に実行中のプロセスでプログラムをデバッグする場合は、通常、次のプロセスに従います。

1. IDE で、[**ツール**] メニューの [**プロセスのデバッグ**] をクリックします。

    **[プロセス]** ダイアログ ボックスが表示されます。

2. プロセスを選択し、[ **アタッチ** ] ボタンをクリックします。

    コンピューターにインストールされているすべてのデバッグエンジン (DEs) を一覧表示 **する [プロセスにアタッチ** ] ダイアログボックスが表示されます。

3. 選択したプロセスのデバッグに使用する DEs を指定し、[ **OK]** をクリックします。

   デバッグパッケージによってデバッグセッションが開始され、DEs の一覧が渡されます。 次に、デバッグセッションがコールバック関数と共にこの一覧を選択されたプロセスに渡し、実行中のプログラムを列挙するようにプロセスに指示します。

   プログラムでは、ユーザーの要求に応じて、デバッグパッケージによってセッションデバッグマネージャー (SDM) がインスタンス化され、選択した DEs の一覧が渡されます。 リストと共に、デバッグパッケージは SDM を [IDebugEventCallback2](../../extensibility/debugger/reference/idebugeventcallback2.md) インターフェイスに渡します。 デバッグパッケージは、 [IDebugProcess2:: Attach](../../extensibility/debugger/reference/idebugprocess2-attach.md)を呼び出して、選択されたプロセスに DEs のリストを渡します。 次に、SDM はポートで [IDebugProcess2:: EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md) を呼び出し、プロセスで実行されているプログラムを列挙します。

   この時点から、各デバッグエンジンは、「 [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)」で詳しく説明されているように、2つの例外を含むプログラムにアタッチされます。

   効率を高めるために、SDM とアドレス空間を共有するために実装されている DEs は、各 DE に、アタッチされるプログラムのセットが含まれるようにグループ化されています。 この場合、 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md) は [IDebugEngine2:: attach](../../extensibility/debugger/reference/idebugengine2-attach.md) を呼び出して、アタッチするプログラムの配列を渡します。

   2つ目の例外は、既に実行されているプログラムへのアタッチ解除によって送信されたスタートアップイベントには、通常、エントリポイントイベントが含まれないことです。

## <a name="see-also"></a>関連項目
- [起動後のスタートアップイベントの送信](../../extensibility/debugger/sending-startup-events-after-a-launch.md)
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
