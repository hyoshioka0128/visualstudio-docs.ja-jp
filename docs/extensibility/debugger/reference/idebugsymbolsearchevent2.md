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
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbe99422e506fb86b0a7e1d9d3242783f3258e6a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80718789"
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

|メソッド|説明|
|------------|-----------------|
|[GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)|シンボル検索の結果に関する情報を取得します。|

## <a name="remarks"></a>注釈
 このイベントは、シンボルの読み込みに失敗した場合でも送信されます。 を呼び出すと、 `IDebugSymbolSearchEvent2::GetSymbolSearchInfo` このイベントのハンドラーは、モジュールに実際にシンボルがあるかどうかを判断できます。

 通常、Visual Studio はこのイベントを使用して、[ **モジュール** ] ウィンドウで読み込まれたシンボルの状態を更新します。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
