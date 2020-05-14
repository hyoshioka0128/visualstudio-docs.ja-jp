---
title: をデバッグブレークポイントエラーイベント2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointErrorEvent2
helpviewer_keywords:
- IDebugBreakpointErrorEvent2
ms.assetid: adee79df-8db5-4510-a7df-c50f4dbf5e35
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 09cb93f0f16420e56104f371d9caab262873390f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735041"
---
# <a name="idebugbreakpointerrorevent2"></a>IDebugBreakpointErrorEvent2
このインターフェイスは、セッション デバッグ マネージャー (SDM) に、保留中のブレークポイントは、警告またはエラーのいずれかのために、読み込まれたプログラムにバインドできませんでしたを指示します。

## <a name="syntax"></a>構文

```
IDebugBreakpointErrorEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、ブレークポイントのサポートの一部としてこのインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります (SDM は、インターフェイス`IDebugEvent2`にアクセスするのに[QueryInterface](/cpp/atl/queryinterface)を使用します)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デは、保留中のブレークポイントをデバッグ中のプログラムにバインドできない場合に、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされたときに、SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugBreakpointErrorEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetErrorBreakpoint](../../../extensibility/debugger/reference/idebugbreakpointerrorevent2-geterrorbreakpoint.md)|警告またはエラーを記述する[IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)インターフェイスを取得します。|

## <a name="remarks"></a>Remarks
 ブレークポイントがバインドされると、イベントが SDM に送信されます。 ブレークポイントをバインドできない場合は、`IDebugBreakpointErrorEvent2`が送信されます。それ以外の場合は[、IDebug ブレークポイントバインドイベント2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)が送信されます。

 たとえば、保留中のブレークポイントに関連付けられている条件が解析または評価に失敗すると、保留中のブレークポイントをこの時点でバインドできないという警告が送信されます。 ブレークポイントのコードがまだ読み込まれていない場合に発生する可能性があります。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugErrorBreakpoint2](../../../extensibility/debugger/reference/idebugerrorbreakpoint2.md)
- [IDebugPendingBreakpoint2](../../../extensibility/debugger/reference/idebugpendingbreakpoint2.md)
- [IDebugBreakpointBoundEvent2](../../../extensibility/debugger/reference/idebugbreakpointboundevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
