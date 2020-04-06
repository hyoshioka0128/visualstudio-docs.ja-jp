---
title: プロパティデストロイイベント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyDestroyEvent2
helpviewer_keywords:
- IDebugPropertyDestroyEvent2 interface
ms.assetid: 301b7a75-ecfa-46f1-9131-66cf3e4be147
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: ce15f389f22513e08b06c0d097cdac4aec3c35bf
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720904"
---
# <a name="idebugpropertydestroyevent2"></a>IDebugPropertyDestroyEvent2
このインターフェイスは、特定のドキュメントに関連付けられているプロパティが破棄されるしようとしているときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugPropertyDestroyEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、プロパティが破棄されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。 このインターフェイスは、DE が以前にスクリプトに関連付けられたプロパティを作成している場合に実装されます。プロパティを破棄すると、関連付けられているスクリプトが IDE から削除されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、プロパティが破棄されたことを報告するために、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされるときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、 の`IDebugPropertyDestroyEvent2`方法を示します。

|Method|説明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertydestroyevent2-getdebugproperty.md)|破棄されるプロパティを取得します。|

## <a name="remarks"></a>Remarks
 これらのイベントが使用される理由の詳細については[、「IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)の解説」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
- [IDebugPropertyCreateEvent2](../../../extensibility/debugger/reference/idebugpropertycreateevent2.md)
