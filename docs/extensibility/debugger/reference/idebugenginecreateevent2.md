---
description: デバッグエンジン (DE) は、DE のインスタンスが作成されるときに、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。
title: IDebugEngineCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEngineCreateEvent2
helpviewer_keywords:
- IDebugEngineCreateEvent2 interface
ms.assetid: 37c0a841-1c8d-4802-a990-36b54bca3ef7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 6155324150b963a5fd26ccecc1244e0792f448bc
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153652"
---
# <a name="idebugenginecreateevent2"></a>IDebugEngineCreateEvent2
デバッグエンジン (DE) は、DE のインスタンスが作成されるときに、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。

## <a name="syntax"></a>構文

```
IDebugEngineCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、通常の操作の一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、メソッドを使用して `QueryInterface` インターフェイスにアクセスし `IDebugEvent2` ます)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 De がインスタンス化されている場合、DE はこのイベントオブジェクトを作成し、送信します。 イベントは、デバッグ対象のプログラムにアタッチされたときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugEngineCreateEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetEngine](../../../extensibility/debugger/reference/idebugenginecreateevent2-getengine.md)|新しく作成されたデバッグエンジン (DE) を表すオブジェクトを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEngine2](../../../extensibility/debugger/reference/idebugengine2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
