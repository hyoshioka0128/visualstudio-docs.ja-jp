---
description: このインターフェイスは、マルチスレッドデバッグをサポートします。
title: IDebugEngineProgram2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ea46ccad8f357cb868a445a8836280abf7c224e0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153379"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
このインターフェイスは、マルチスレッドデバッグをサポートします。

## <a name="syntax"></a>構文

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジンは、複数のスレッドの同時デバッグをサポートするために、このインターフェイスを実装します。 このインターフェイスは、 [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md) インターフェイスを実装するのと同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [QueryInterface](/cpp/atl/queryinterface)を使用して、インターフェイスからこのインターフェイスを取得し `IDebugProgram2` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEngineProgram2` ます。

|メソッド|説明|
|------------|-----------------|
|[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|このプログラムで実行されているすべてのスレッドを停止します。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|指定されたスレッドで実行を監視します (または実行の監視を停止します)。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|プログラムが停止している場合でも、指定したスレッドで式の評価を実行できるようにします (または禁止します)。|

## <a name="remarks"></a>解説
 Visual Studio は、 [IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md) イベントに応答してこのインターフェイスを呼び出し、"スレッドのウォッチ" ステップと "スレッドでの式の評価を監視する" というプログラムの状態を設定します。 [Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md) は、プログラムが停止されるたびに呼び出されます。このメソッドは、プログラムがすべてのスレッドを終了する機会を提供します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
