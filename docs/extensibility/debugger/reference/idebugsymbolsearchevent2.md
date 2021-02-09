---
title: IDebugSymbolSearchEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugSymbolSearchEvent2
helpviewer_keywords:
- IDebugSymbolSearchEvent2
ms.assetid: 9b946d55-ff85-44eb-b40a-efbf8282eafd
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: ad5fa763be8929a9122a6fd7517b401f5a874e04
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909343"
---
# <a name="idebugsymbolsearchevent2"></a>IDebugSymbolSearchEvent2
このインターフェイスは、デバッグエンジン (DE) によって送信され、デバッグされているモジュールのデバッグシンボルが読み込まれたことを示します。

## <a name="syntax"></a>構文

```
IDebugSymbolSearchEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、モジュールのシンボルが読み込まれたことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、モジュールのシンボルが読み込まれたことを報告するために、このイベントオブジェクトを作成して送信します。 イベントは、デバッグ対象のプログラムにアタッチされたときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスは、 `IDebugSymbolSearchEvent2` 次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|シンボル検索の結果に関する情報を取得します。|

## <a name="remarks"></a>解説
 このイベントは、シンボルの読み込みに失敗した場合でも送信されます。 を呼び出すと、 `IDebugSymbolSearchEvent2::GetSymbolSearchInfo` このイベントのハンドラーは、モジュールに実際にシンボルがあるかどうかを判断できます。

 通常、Visual Studio はこのイベントを使用して、[ **モジュール** ] ウィンドウで読み込まれたシンボルの状態を更新します。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
