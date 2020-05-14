---
title: プログラム2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineProgram2
helpviewer_keywords:
- IDebugEngineProgram2 interface
ms.assetid: 151003a9-2e4d-4acf-9f4d-365dfa6b9596
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 8e5ccf2327e660a983bcb3032363a92ac8a6f71d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730299"
---
# <a name="idebugengineprogram2"></a>IDebugEngineProgram2
このインターフェイスは、マルチスレッド デバッグのサポートを提供します。

## <a name="syntax"></a>構文

```
IDebugEngineProgram2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジンは、複数のスレッドの同時デバッグをサポートするために、このインターフェイスを実装します。 このインターフェイスは[、IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)インターフェイスを実装する同じオブジェクトに実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を`IDebugProgram2`使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugEngineProgram2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Stop](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)|このプログラムで実行中のすべてのスレッドを停止します。|
|[WatchForThreadStep](../../../extensibility/debugger/reference/idebugengineprogram2-watchforthreadstep.md)|指定されたスレッドで実行を監視 (または実行の監視を停止) します。|
|[WatchForExpressionEvaluationOnThread](../../../extensibility/debugger/reference/idebugengineprogram2-watchforexpressionevaluationonthread.md)|プログラムが停止している場合でも、指定されたスレッドで式の評価を行うことを許可します (または、許可しません)。|

## <a name="remarks"></a>Remarks
 Visual Studio は[、IDebugProgramCreateEvent2](../../../extensibility/debugger/reference/idebugprogramcreateevent2.md)イベントに応答して、プログラムの "スレッド ステップの監視" および "スレッドの式評価を監視" 状態を設定するために、このインターフェイスを呼び出します。 [停止](../../../extensibility/debugger/reference/idebugengineprogram2-stop.md)は、プログラムを停止する場合には常に呼び出されます。このメソッドは、プログラムにすべてのスレッドを終了する機会を与えます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugProgram2](../../../extensibility/debugger/reference/idebugprogram2.md)
