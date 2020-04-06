---
title: 必要なポートサプライヤーインターフェイス |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: conceptual
helpviewer_keywords:
- port suppliers, required interfaces
- debugging [Debugging SDK], port suppliers
ms.assetid: 0c2cdd40-9f6f-425e-b305-858f7734161e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: bf2aeb1f26f81d773e171aa3fed6b0f2ef976c91
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80713153"
---
# <a name="required-port-supplier-interfaces"></a>必要なポート サプライヤー インターフェイス
ポート サプライヤーは[、IDebugPortSupplier2](../../extensibility/debugger/reference/idebugportsupplier2.md)インターフェイスを実装する必要があります。[IDebug ポートサプライヤー2](../../extensibility/debugger/reference/idebugportsupplier2.md)

 ポート サプライヤは、ポートを供給し、それらを実装します。 したがって、次のインターフェイスを実行する必要があります。

- [IDebugPort2](../../extensibility/debugger/reference/idebugport2.md)

  ポートについて説明し、ポートで実行されているすべてのプロセスを列挙します。

- [IDebugPortEx2](../../extensibility/debugger/reference/idebugportex2.md)

  ポート上でプロセスを起動および終了するための機能を提供します。

- [IDebugPortNotify2](../../extensibility/debugger/reference/idebugportnotify2.md)

  このポートのコンテキスト内で実行されているプログラムが、プログラム ノードの作成と破棄を通知するメカニズムを提供します。 詳しくは、[プログラム・ノードを](../../extensibility/debugger/program-nodes.md)参照してください。

- `IConnectionPointContainer`

  のコネクション[ポイントを提供](../../extensibility/debugger/reference/idebugportevents2.md)します。

## <a name="port-supplier-operation"></a>港湾サプライヤーの運営
 [IDebugPortEvents2](../../extensibility/debugger/reference/idebugportevents2.md)シンクは、プロセスとプログラムがポートで作成および破棄されたときに通知を受け取ります。 プロセスが作成されたときに[IDebugProcessCreateEvent2](../../extensibility/debugger/reference/idebugprocesscreateevent2.md)を送信するにはポートが必要であり、ポートでプロセスが破棄されたときに[IDebugProcessDestroyEvent2](../../extensibility/debugger/reference/idebugprocessdestroyevent2.md)が必要です。 また、プログラムが作成されたときに[IDebugProgramCreateEvent2](../../extensibility/debugger/reference/idebugprogramcreateevent2.md)を送信するためにポートが必要であり、ポートで実行されているプロセスでプログラムが破棄されたときに[IDebugProgramDestroyEvent2](../../extensibility/debugger/reference/idebugprogramdestroyevent2.md)が必要です。

 ポートは通常、プログラムの作成と破棄のイベントをそれぞれ[送信](../../extensibility/debugger/reference/idebugportnotify2-addprogramnode.md)します。 [RemoveProgramNode](../../extensibility/debugger/reference/idebugportnotify2-removeprogramnode.md)

 ポートは物理プロセスと論理プログラムの両方を起動および終了できるため、デバッグ エンジンによって次のインターフェイスも実装する必要があります。

- [IDebugProcess2](../../extensibility/debugger/reference/idebugprocess2.md)

  物理プロセスについて説明します。 少なくとも以下のメソッドを実装する必要があります。

  - [EnumPrograms](../../extensibility/debugger/reference/idebugprocess2-enumprograms.md)

  - [GetName](../../extensibility/debugger/reference/idebugprocess2-getname.md)

  - [GetServer](../../extensibility/debugger/reference/idebugprocess2-getserver.md)

  - [GetPhysicalProcessId](../../extensibility/debugger/reference/idebugprocess2-getphysicalprocessid.md)

  - [プロセス ID を取得します。](../../extensibility/debugger/reference/idebugprocess2-getprocessid.md)

  - [GetAttachedSessionName](../../extensibility/debugger/reference/idebugprocess2-getattachedsessionname.md)

- [IDebugProcessEx2](../../extensibility/debugger/reference/idebugprocessex2.md)

  SDM がプロセスにアタッチして、プロセスからデタッチする方法を提供します。

- [IDebugProgram2](../../extensibility/debugger/reference/idebugprogram2.md)

  論理プログラムについて説明します。 少なくとも以下のメソッドを実装する必要があります。

  - [GetName](../../extensibility/debugger/reference/idebugprogram2-getname.md)

  - [プロセスを取得します。](../../extensibility/debugger/reference/idebugprogram2-getprocess.md)

  - [GetProgramId](../../extensibility/debugger/reference/idebugprogram2-getprogramid.md)

- [IDebugProgramEx2](../../extensibility/debugger/reference/idebugprogramex2.md)

  SDM がこのプログラムにアタッチする方法を提供します。

## <a name="see-also"></a>関連項目
- [ポート サプライヤーの実装](../../extensibility/debugger/implementing-a-port-supplier.md)
