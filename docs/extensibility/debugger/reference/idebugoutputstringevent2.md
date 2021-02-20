---
title: IDebugOutputStringEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugOutputStringEvent2
helpviewer_keywords:
- IDebugOutputStringEvent2 interface
ms.assetid: 86596fd1-cecc-4813-8add-dc3d70068f9b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 8fa51311bb7548889cccdd2eb91e70a4679fb5de
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99953306"
---
# <a name="idebugoutputstringevent2"></a>IDebugOutputStringEvent2
このインターフェイスは、文字列を出力するために、デバッグエンジン (DE) によってセッションデバッグマネージャー (SDM) に送信されます。

## <a name="syntax"></a>構文

```
IDebugOutputStringEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、このインターフェイスを実装して、IDE の **出力** ウィンドウに文字列を送信します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成し、 **出力** ウィンドウに文字列を送信するために送信します。 イベントは、デバッグ対象のプログラムにアタッチされているときに、SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表は、のメソッドを示して `IDebugOutputStringEvent2` います。

|Method|説明|
|------------|-----------------|
|[GetString](../../../extensibility/debugger/reference/idebugoutputstringevent2-getstring.md)|表示可能メッセージを取得します。|

## <a name="remarks"></a>解説
 たとえば、アンマネージコードでは、デバッグ中のプログラムが Win32 関数に文字列を送信したときに出力される文字列が生成され `OutputDebugString` ます。 この文字列は DE によってインターセプトされ、イベントとして SDM に送信され `IDebugOutputStringEvent2` ます。

 [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)を使用して、ユーザーの応答を必要とするメッセージを送信します。

 [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)を使用して、応答を必要としないエラーメッセージを送信します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugMessageEvent2](../../../extensibility/debugger/reference/idebugmessageevent2.md)
- [IDebugErrorEvent2](../../../extensibility/debugger/reference/idebugerrorevent2.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
