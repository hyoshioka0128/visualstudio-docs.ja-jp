---
title: ポートへの通知 |Microsoft Docs
description: プログラムを起動した後、ポートに通知する方法について説明します。 この記事には、詳細な説明が含まれています。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- ports, notification
ms.assetid: f9fce48e-7d4e-4627-a0fb-77b75428146a
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7793dddb1a6bdd448b2b5a912f59b625bdca733e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054752"
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

## <a name="see-also"></a>こちらもご覧ください
- [プログラムの起動](../../extensibility/debugger/launching-a-program.md)
- [起動後のアタッチ](../../extensibility/debugger/attaching-after-a-launch.md)
- [デバッグタスク](../../extensibility/debugger/debugging-tasks.md)
