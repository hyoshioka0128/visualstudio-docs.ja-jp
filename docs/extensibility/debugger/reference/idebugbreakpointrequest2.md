---
title: Iデバッグブレークポイントリクエスト2 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBreakpointRequest2
helpviewer_keywords:
- IDebugBreakpointRequest2 interface
ms.assetid: 01ac4013-96f9-4235-b289-f55f9e99558f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: f30f9698c9c81322edd6935b40c16cad6f46024c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734921"
---
# <a name="idebugbreakpointrequest2"></a>IDebugBreakpointRequest2
このインターフェイスは、任意の種類のブレークポイントを作成およびバインドするために必要な情報を表します。

## <a name="syntax"></a>構文

```
IDebugBreakpointRequest2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 セッション デバッグ マネージャー (SDM) は、通常、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 デバッグ エンジン (DE) は、保留中のブレークポイントを作成するために[CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)の呼び出しを通じてこのインターフェイスを受信します。 呼び出しは DE からこのインターフェイスを取得できます[。](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugBreakpointRequest2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetLocationType](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getlocationtype.md)|このブレークポイント要求のブレークポイントの場所の種類を取得します。|
|[GetRequestInfo](../../../extensibility/debugger/reference/idebugbreakpointrequest2-getrequestinfo.md)|このブレークポイント要求を記述するブレークポイント要求情報を取得します。|

## <a name="remarks"></a>Remarks
 デバッグ中のプログラムが読み込まれた後[、Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)の呼び出しは、保留中のブレークポイントをプログラム内の要求された場所にバインドします。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [CreatePendingBreakpoint](../../../extensibility/debugger/reference/idebugengine2-creatependingbreakpoint.md)
- [GetBreakpointRequest](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-getbreakpointrequest.md)
- [Bind](../../../extensibility/debugger/reference/idebugpendingbreakpoint2-bind.md)
