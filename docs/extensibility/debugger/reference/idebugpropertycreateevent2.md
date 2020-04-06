---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84d8fcb4375f29820b51752ac3fdebbd04f06f80
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720932"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
このインターフェイスは、特定のドキュメントに関連付けられているプロパティを作成するときに、デバッグ エンジン (DE) によってセッション デバッグ マネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugPropertyCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、プロパティが作成されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。 このインターフェイスは、読み込みまたは作成されたスクリプトに関連付けられたプロパティが DE によって作成され、そのスクリプトを IDE に表示する必要がある場合に実装されます。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、このイベント オブジェクトを作成して送信し、プロパティが作成されたことを報告します。 イベントは、デバッグ中のプログラムにアタッチされるときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、インターフェイスのメソッド`IDebugPropertyCreateEvent2`を示します。

|Method|説明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|新しいプロパティを取得します。|

## <a name="remarks"></a>Remarks
 プロパティに特定のドキュメントまたはスクリプトが関連付けられている場合、DE は、このイベントを SDM に送信して、ドキュメントの名前を使用して **[スクリプト ドキュメント]** ウィンドウを更新できます。 SDM は、IUnknown ポインターを含`guidDocument`むを取得`VARIANT`する引数[IUnknown](/cpp/atl/iunknown)を使用して[GetExtendedInfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md)を呼び出します。 SDM は、このポインターで[クエリ インターフェイス](/cpp/atl/queryinterface)を呼び出して、**スクリプト ドキュメント**ウィンドウの更新に使用される[IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスを取得します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
