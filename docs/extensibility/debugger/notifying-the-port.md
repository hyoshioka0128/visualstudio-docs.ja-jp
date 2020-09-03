---
title: ポートへの通知 |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80738318"
---
# <a name="notify-the-port"></a>ポートに通知する
プログラムを起動した後、次のようにポートに通知する必要があります。

1. ポートは、新しいプログラムノードを受け取ると、デバッグセッションにプログラム作成イベントを送り返します。 このイベントには、プログラムを表すインターフェイスが含まれています。

2. デバッグセッションは、にアタッチできるデバッグエンジン (DE) の識別子をプログラムに対して照会します。

3. デバッグセッションは、そのプログラムの使用可能な DEs の一覧に DE があるかどうかを確認します。 デバッグセッションでは、ソリューションのアクティブなプログラム設定からこのリストを取得します。この設定は、最初はデバッグパッケージによって渡されます。

    DE は許可リストに存在する必要があります。そうでない場合、DE はプログラムにアタッチされません。

   プログラムによって、ポートが最初に新しいプログラムノードを受け取ると、プログラムを表す [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスが作成されます。

> [!NOTE]
> これは、 `IDebugProgram2` 後でデバッグエンジン (DE) によって作成されたインターフェイスと混同しないようにしてください。

 ポートは、COM インターフェイスを介して [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) プログラム作成イベントをセッションデバッグマネージャー (SDM) に送り返し `IConnectionPoint` ます。

> [!NOTE]
> これは、 `IDebugProgramCreateEvent2` 後で DE によって送信されるインターフェイスと混同しないようにしてください。

 ポートは、イベントインターフェイス自体と共に、 [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)、 [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)、および [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md) の各インターフェイスを送信します。これらのインターフェイスは、それぞれポート、プロセス、およびプログラムを表します。 SDM は [IDebugProgram2:: GetEngineInfo](../../extensibility/debugger/reference/idebugprogram2-getengineinfo.md) を呼び出して、プログラムをデバッグできる DE の GUID を取得します。 GUID はもともと、 [IDebugProgramNode2](../../extensibility/debugger/reference/idebugprogramnode2.md) インターフェイスから取得されています。

 SDM は、DE が許可されている DEs の一覧にあるかどうかを確認します。 SDM は、ソリューションのアクティブなプログラム設定からこのリストを取得します。この設定は、最初はデバッグパッケージによって渡されます。 DE は許可リストに存在する必要があります。そうでない場合は、プログラムにアタッチされません。

 DE の id がわかったら、SDM はプログラムにアタッチする準備ができています。

## <a name="see-also"></a>関連項目
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
- [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
