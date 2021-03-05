---
description: このインターフェイスは、モジュール (つまり、DLL などのプログラムの実行可能単位) を表します。
title: IDebugModule2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b7cc14d4f33924a04b25344c4c624a633b97ff7b
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150485"
---
# <a name="idebugmodule2"></a>IDebugModule2
このインターフェイスは、モジュール (つまり、DLL などのプログラムの実行可能単位) を表します。

## <a name="syntax"></a>構文

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、モジュールを表し、そのモジュールに関する情報へのアクセスを提供するために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getmodule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)を呼び出すと、このインターフェイスが返されます。 DE は、[イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)メソッドを使用して、 [IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)インターフェイスをセッションデバッグマネージャー (SDM) に送信します。

 このインターフェイスは、 [フレーム情報](../../../extensibility/debugger/reference/frameinfo.md) 構造体 ( [enumフレーム情報](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)の呼び出しによって返される) でも返すことができます。

- [次](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md) に、このインターフェイスも返します ([Enummodules](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) は [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md) インターフェイスを返します)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugModule2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|このモジュールを説明する [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md) を取得します。|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|互換性のために残されています。 使用しないでください。 このモジュールのシンボルを再読み込みします。|

## <a name="remarks"></a>解説
 モジュール情報は、IDE の [ **モジュール** ] ウィンドウに表示できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetModule](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
