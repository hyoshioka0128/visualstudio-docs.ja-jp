---
title: IDebugBreakpointErrorEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2
helpviewer_keywords:
- IDebugBreakpointErrorEvent2
ms.assetid: adee79df-8db5-4510-a7df-c50f4dbf5e35
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 033c997f3bd1038c2103a6c0ef3ad9ddbd74c249
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99901861"
---
# <a name="idebugbreakpointerrorevent2"></a>IDebugBreakpointErrorEvent2
このインターフェイスは、警告またはエラーのために、読み込まれたプログラムに保留中のブレークポイントをバインドできなかったことをセッションデバッグマネージャー (SDM) に通知します。

## <a name="syntax"></a>構文

```
IDebugBreakpointErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、ブレークポイントのサポートの一部として、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は[QueryInterface](/cpp/atl/queryinterface)を使用してインターフェイスにアクセスし `IDebugEvent2` ます)。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、デバッグ中のプログラムに保留中のブレークポイントをバインドできない場合に、このイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされるときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBreakpointErrorEvent2` ます。

|Method|説明|
|------------|-----------------|
|[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)|警告またはエラーを説明する [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md) インターフェイスを取得します。|

## <a name="remarks"></a>解説
 ブレークポイントがバインドされるたびに、イベントが SDM に送信されます。 ブレークポイントをバインドできない場合は、が送信されます。 `IDebugBreakpointErrorEvent2` それ以外の場合は、 [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md) が送信されます。

 たとえば、保留中のブレークポイントに関連付けられている条件が解析または評価に失敗した場合、この時点では、保留中のブレークポイントをバインドできないという警告が送信されます。 これは、ブレークポイントのコードがまだ読み込まれていない場合に発生する可能性があります。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
