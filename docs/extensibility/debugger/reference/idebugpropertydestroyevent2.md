---
description: このインターフェイスは、特定のドキュメントに関連付けられているプロパティが破棄されるときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。
title: IDebugPropertyDestroyEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyDestroyEvent2
helpviewer_keywords:
- IDebugPropertyDestroyEvent2 interface
ms.assetid: 301b7a75-ecfa-46f1-9131-66cf3e4be147
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: d9d0e0751b184ddbf6ebc62e12ed1d3a9bca853c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105083805"
---
# <a name="idebugpropertydestroyevent2"></a>IDebugPropertyDestroyEvent2
このインターフェイスは、特定のドキュメントに関連付けられているプロパティが破棄されるときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>Syntax

```
IDebugPropertyDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、プロパティが破棄されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。 このインターフェイスは、スクリプトに関連付けられたプロパティを DE が以前に作成した場合に実装されます。プロパティを破棄すると、関連付けられているスクリプトが IDE から削除されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成し、プロパティを報告するために送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、のメソッドを示して `IDebugPropertyDestroyEvent2` います。

|メソッド|説明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertydestroyevent2-getdebugproperty.md)|破棄されるプロパティを取得します。|

## <a name="remarks"></a>注釈
 これらのイベントが使用される理由の詳細については、 [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md) の解説を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)
