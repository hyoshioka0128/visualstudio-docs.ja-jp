---
description: このインターフェイスは、スレッドの実行が完了すると、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。
title: IDebugThreadDestroyEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThreadDestroyEvent2
helpviewer_keywords:
- IDebugThreadDestroyEvent2
ms.assetid: fca3f603-9432-457b-9ddd-8b0ec17da046
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 48390b220a1398e712af494a6d0f21024f659f49
ms.sourcegitcommit: f33ca1fc99f5d9372166431cefd0e0e639d20719
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102223122"
---
# <a name="idebugthreaddestroyevent2"></a>IDebugThreadDestroyEvent2
このインターフェイスは、スレッドの実行が完了すると、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugThreadDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、スレッドが終了したことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成して送信し、スレッドが終了したことを報告します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugThreadDestroyEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetExitCode](../../../extensibility/debugger/reference/idebugthreaddestroyevent2-getexitcode.md)|スレッドの終了コードを取得します。|

## <a name="remarks"></a>解説
 Visual Studio では、このイベントを使用して [ **スレッド** ] ウィンドウを更新します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugThread2](../../../extensibility/debugger/reference/idebugthread2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
