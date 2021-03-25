---
title: 必要なポート供給業者インターフェイス |Microsoft Docs
description: ポートサプライヤーが実行する必要のあるインターフェイスについて説明します。 ポートサプライヤーはポートを提供し、それらを実装します。
ms.custom: SEO-VS-2020
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 1f5755ce47a2b76c9a0d38b1f7eed3b38d64c876
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105070610"
---
# <a name="required-port-supplier-interfaces"></a>必要なポート供給業者インターフェイス
ポートサプライヤーは、 [IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md) インターフェイスを実装する必要があります。[IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 ポートサプライヤーはポートを提供し、それらを実装します。 したがって、次のインターフェイスを実行する必要があります。

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  ポートについて説明し、ポートで実行されているすべてのプロセスを列挙します。

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  ポートでプロセスを起動および終了するためのを提供します。

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  このポートのコンテキスト内で実行されるプログラムに対して、プログラムノードの作成と破棄を通知するためのメカニズムを提供します。 詳細については、「 [プログラムノード](../../extensibility/debugger/program-nodes.md)」を参照してください。

- `IConnectionPointContainer`

  [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)の接続ポイントを提供します。

## <a name="port-supplier-operation"></a>ポートサプライヤー操作
 プロセスとプログラムが作成され、ポートで破棄されると、 [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md) シンクは通知を受信します。 ポートは、プロセスが作成されたときに [IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md) を送信するために必要であり、ポートでプロセスが破棄されるときに [IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md) されます。 また、ポートは、プログラムが作成されたときに [IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md) を送信するために必要であり、ポートで実行されているプロセスでプログラムが破棄されると [IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md) します。

 通常、ポートは、 [addprogramnode](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md) メソッドと [removeprogramnode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md) メソッドに応答してプログラム作成イベントと破棄イベントを送信します。

 ポートは物理プロセスと論理プログラムの両方を起動して終了できるため、次のインターフェイスもデバッグエンジンによって実装される必要があります。

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)

  物理プロセスについて説明します。 少なくとも次のメソッドを実装する必要があります。

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)

  - [GetProcessId](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)

  SDM をプロセスからアタッチおよびデタッチする方法を提供します。

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)

  論理プログラムについて説明します。 少なくとも次のメソッドを実装する必要があります。

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)

  - [GetProcess](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)

- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)

  SDM をこのプログラムにアタッチする方法を提供します。

## <a name="see-also"></a>こちらもご覧ください
- [ポートサプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)
