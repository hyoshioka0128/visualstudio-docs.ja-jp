---
title: をクリックして実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule3
helpviewer_keywords:
- IDebugModule3 interface
ms.assetid: 44f8e96e-9c59-4ffc-9a08-9c908a0e4de7
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 84db1b672a9460ef3809162a2a1433f269796046
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726735"
---
# <a name="idebugmodule3"></a>IDebugModule3
このインターフェイスは、シンボルと JustMyCode 状態の代替の場所をサポートするモジュールを表します。

## <a name="syntax"></a>構文

```
IDebugModule3 : IDebugModule2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、シンボルの代替場所をサポートし、JustMyCode 状態を操作するこのインターフェイスを実装します (「JustMyCode」の定義については[、Visual Studio デバッガーの用語集](../../../extensibility/debugger/reference/visual-studio-debugger-glossary.md)を参照してください)。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [呼](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)び出しは、このインターフェイスを返します。 DE は[、イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)メソッドを使用してセッション デバッグ マネージャー (SDM) に[IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)インターフェイスを送信します。 また[、IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)インターフェイスで[のクエリ インターフェイス](/cpp/atl/queryinterface)の呼び出しは、このインターフェイスを返します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは[、IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)インターフェイスのメソッドに加えて、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetSymbolInfo](../../../extensibility/debugger/reference/idebugmodule3-getsymbolinfo.md)|シンボルを検索したパスのリストと、各パスの検索結果を返します。|
|[LoadSymbols](../../../extensibility/debugger/reference/idebugmodule3-loadsymbols.md)|現在のモジュールのシンボルを読み込んで初期化します。|
|[IsUserCode](../../../extensibility/debugger/reference/idebugmodule3-isusercode.md)|モジュールがユーザー コードを表すかどうかを示すフラグを返します。|
|[SetJustMyCodeState](../../../extensibility/debugger/reference/idebugmodule3-setjustmycodestate.md)|モジュールをユーザー コードと見なすかどうかを指定します。|

## <a name="remarks"></a>Remarks
 Visual Studio は、このインターフェイスの一般的なコンシューマーです。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugModule2](../../../extensibility/debugger/reference/idebugmodule2.md)
- [IDebugSymbolSearchEvent2](../../../extensibility/debugger/reference/idebugsymbolsearchevent2.md)
- [GetSymbolSearchInfo](../../../extensibility/debugger/reference/idebugsymbolsearchevent2-getsymbolsearchinfo.md)
