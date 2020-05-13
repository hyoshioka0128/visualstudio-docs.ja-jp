---
title: を返す値イベント2 を返す |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugReturnValueEvent2
helpviewer_keywords:
- IDebugReturnValueEvent2
ms.assetid: 2daded43-e427-4fbb-a19e-f3834e3723af
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d0afc4284795ae8dcae7b41d9207ddc6e7c11e67
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720252"
---
# <a name="idebugreturnvalueevent2"></a>IDebugReturnValueEvent2
このインターフェイスは、関数のステップ アウトまたは上のステップの後にセッション デバッグ マネージャー (SDM) にデバッグ エンジン (DE) によって送信されます。

## <a name="syntax"></a>構文

```
IDebugReturnValueEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、このインターフェイスを実装して、ステップ アウトまたはステップ オーバーされた関数からの戻り値を報告します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、関数の戻り値を報告するために、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされるときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、 の`IDebugReturnValueEvent2`方法を示します。

|Method|説明|
|------------|-----------------|
|[GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)|関数からステップ アウトしたときに返される値を取得します。|

## <a name="remarks"></a>Remarks
 関数から返される値は、 [GetReturnValue](../../../extensibility/debugger/reference/idebugreturnvalueevent2-getreturnvalue.md)を呼び出すことによって取得できます。 返された値は **[自動変数**]ウィンドウに表示されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
