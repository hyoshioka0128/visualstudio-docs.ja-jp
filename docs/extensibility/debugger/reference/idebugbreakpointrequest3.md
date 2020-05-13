---
title: Iデバッグブレークポイントリクエスト3 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest3
helpviewer_keywords:
- IDebugBreakpointRequest3
ms.assetid: 8a042beb-b319-48e3-b3c8-9c8336ab371b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 505b0c0b05fa0f14578d770abec6c43ed6b80b01
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734819"
---
# <a name="idebugbreakpointrequest3"></a>IDebugBreakpointRequest3
このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。 これは[、IDebug ブレークポイント要求2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)の拡張機能です。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest3 : IDebugBreakpointRequest2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 セッション デバッグ マネージャー (SDM) は、通常、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デバッグ エンジン (DE) は、呼び出しで受信した IDebugBreakpointRequest2 インターフェイスで[クエリ インターフェイス](/cpp/atl/queryinterface)を呼び出すことによって、このインターフェイスにアクセス[します](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [から](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)継承されたメソッドに加えて、インターフェイスは`IDebugBreakpointRequest3`、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[GetRequestInfo2](../../../extensibility/debugger/reference/idebugbreakpointrequest3-getrequestinfo2.md)|このブレークポイント要求を記述するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは[、BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)構造体を通じて DE に追加情報を提供するために使用されます。 この追加情報には、DE のベンダ ID (GUID の形式)、トレースポイントの名前、およびブレークポイント制約の名前が含まれます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugBreakpointRequest2](../../../extensibility/debugger/reference/idebugbreakpointrequest2.md)
- [BP_REQUEST_INFO2](../../../extensibility/debugger/reference/bp-request-info2.md)
