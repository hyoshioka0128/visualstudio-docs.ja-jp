---
title: を読み込むイベント 2 を実行するマイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModuleLoadEvent2
helpviewer_keywords:
- IDebugModuleLoadEvent2 interface
ms.assetid: 7d26fb23-5d49-4ba7-b7c5-3aed4d7be81e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 06bb96d8a02ccc9299d43f28b4fbfa3fdb39acdc
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726703"
---
# <a name="idebugmoduleloadevent2"></a>IDebugModuleLoadEvent2
このインターフェイスは、デバッグ エンジン (DE) によって、セッション デバッグ マネージャー (SDM) モジュールが読み込まれるか、またはアンロードされたときに送信されます。

## <a name="syntax"></a>構文

```
IDebugModuleLoadEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、モジュールがロードまたはアンロードされたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、モジュールがロードまたはアンロードされたことを報告するために、このイベント オブジェクトを作成して送信します。 イベントは、デバッグ中のプログラムにアタッチされるときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、 の`IDebugModuleLoadEvent2`方法を示します。

|Method|説明|
|------------|-----------------|
|[モジュールを取得します。](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)|読み込みまたはアンロードされているモジュールを取得します。|

## <a name="remarks"></a>Remarks
 Visual Studio では、このイベントを**使用してモジュール**ウィンドウを最新の状態に保ちます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
