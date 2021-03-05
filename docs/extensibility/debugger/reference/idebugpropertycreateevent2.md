---
description: このインターフェイスは、特定のドキュメントに関連付けられているプロパティを作成するときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。
title: IDebugPropertyCreateEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyCreateEvent2
helpviewer_keywords:
- IDebugPropertyCreateEvent2 interface
ms.assetid: 33b3082b-a42e-488a-a1e4-dadf506f922c
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 0a8a4317ec3e1c2c83becf0bffb5274ae5a44cf4
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102168050"
---
# <a name="idebugpropertycreateevent2"></a>IDebugPropertyCreateEvent2
このインターフェイスは、特定のドキュメントに関連付けられているプロパティを作成するときに、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugPropertyCreateEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、プロパティが作成されたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。 このインターフェイスは、読み込みまたは作成されたスクリプトに関連付けられたプロパティを DE が作成した場合、およびそのスクリプトを IDE に表示する必要がある場合に実装されます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成し、プロパティが作成されたことを報告するように送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、インターフェイスのメソッドを示して `IDebugPropertyCreateEvent2` います。

|メソッド|説明|
|------------|-----------------|
|[GetDebugProperty](../../../extensibility/debugger/reference/idebugpropertycreateevent2-getdebugproperty.md)|新しいプロパティを取得します。|

## <a name="remarks"></a>解説
 プロパティに特定のドキュメントまたはスクリプトが関連付けられている場合、DE はこのイベントを SDM に送信して、 **スクリプトドキュメント** ウィンドウをドキュメントの名前で更新することができます。 SDM は、引数を指定して [Getextendedinfo](../../../extensibility/debugger/reference/idebugproperty2-getextendedinfo.md) を呼び出し、 `guidDocument` `VARIANT` [IUnknown](/cpp/atl/iunknown) ポインターを含むを取得します。 SDM は、このポインターの [QueryInterface](/cpp/atl/queryinterface)を呼び出して、[**スクリプトドキュメント**] ウィンドウの更新に使用される [IDebugDocument2](../../../extensibility/debugger/reference/idebugdocument2.md)インターフェイスを取得します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
- [IDebugProperty2](../../../extensibility/debugger/reference/idebugproperty2.md)
