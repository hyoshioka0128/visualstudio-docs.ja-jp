---
title: ポートへの通知 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ff94c20969e77bcc70af2f5a16137e09366a0d7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80738318"
---
# <a name="notify-the-port"></a>ポートに通知する
プログラムを起動した後、ポートに次のように通知する必要があります。

1. ポートは、新しいプログラム ノードを受信すると、プログラム作成イベントをデバッグ セッションに送り返します。 イベントは、プログラムを表すインターフェイスを持ちます。

2. デバッグ セッションは、アタッチできるデバッグ エンジン (DE) の識別子をプログラムに照会します。

3. デバッグ セッションは、DE がそのプログラムで許容される DE の一覧にあるかどうかを確認します。 デバッグ セッションは、デバッグ パッケージによって元々渡される、ソリューションのアクティブなプログラム設定からこの一覧を取得します。

    DE は許容リストに含める必要があります。

   プログラムを使用すると、ポートが最初に新しいプログラム ノードを受信したときに、プログラムを表す[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスが作成されます。

> [!NOTE]
> これは、デバッグ エンジン (DE) によって後で`IDebugProgram2`作成されるインターフェイスと混同しないでください。

 ポートは、COM`IConnectionPoint`インターフェイスを使用してセッション デバッグ マネージャー (SDM) に[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)プログラム作成イベントを送信します。

> [!NOTE]
> これは、後で`IDebugProgramCreateEvent2`DE によって送信されるインターフェイスと混同しないでください。

 イベント インターフェイス自体と共に、ポートは、それぞれポート、プロセス、およびプログラムを表す[IDebugPort2](../../extensibility/debugger/reference/idebugport2.md) [、IDebugProcess2、](../../extensibility/debugger/reference/idebugprocess2.md)および[IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスを送信します。 SDM は、プログラムをデバッグできる DE の GUID を取得するために[IDebugProgram2::GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md)を呼び出します。 GUID はもともと[IDebug プログラムノード2](../../extensibility/debugger/reference/idebugprogramnode2.md)インターフェイスから取得されました。

 SDM は、DE が許容可能な DE のリストにあるかどうかを確認します。 SDM は、ソリューションのアクティブなプログラム設定からこのリストを取得します。 DE は許容リストに含める必要があります。

 DE の ID が認識されると、SDM はプログラムにアタッチする準備が整います。

## <a name="see-also"></a>関連項目
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
- [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)
- [デバッグ タスク](../../extensibility/debugger/debugging-tasks.md)
