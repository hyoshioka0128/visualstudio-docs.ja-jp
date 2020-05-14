---
title: をクリックして実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugModule2
helpviewer_keywords:
- IDebugModule2 interface
ms.assetid: 24c2a126-f4ab-4891-8509-8ef99b994c08
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dbbea1b52133de41dd26f437aeba31a0eff5a50a
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726910"
---
# <a name="idebugmodule2"></a>IDebugModule2
このインターフェイスは、DLL などのモジュール (プログラムの実行可能単位) を表します。

## <a name="syntax"></a>構文

```
IDebugModule2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、モジュールを表し、そのモジュールに関する情報へのアクセスを提供するこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 呼び出しは[、この](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)インターフェイスを返します。 DE は[、イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)メソッドを使用してセッション デバッグ マネージャー (SDM) に[IDebugModuleLoadEvent2](../../../extensibility/debugger/reference/idebugmoduleloadevent2.md)インターフェイスを送信します。

 このインターフェイスは[、(EnumFrameInfo](../../../extensibility/debugger/reference/frameinfo.md)への呼び出しによって返される) [EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)FRAMEINFO 構造体で返すこともできます。

- [次に](../../../extensibility/debugger/reference/ienumdebugmodules2-next.md)、このインターフェイスも返します ([列挙モジュールは](../../../extensibility/debugger/reference/idebugprogram2-enummodules.md) [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)インターフェイスを返します)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugModule2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)|このモジュールを説明する[MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)を取得します。|
|[ReloadSymbols_Deprecated](../../../extensibility/debugger/reference/idebugmodule2-reloadsymbols-deprecated.md)|廃止。 使用しないでください。 このモジュールのシンボルを再ロードします。|

## <a name="remarks"></a>Remarks
 モジュール情報は、IDE の **「モジュール」** ウィンドウに表示できます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [モジュールを取得します。](../../../extensibility/debugger/reference/idebugmoduleloadevent2-getmodule.md)
- [FRAMEINFO](../../../extensibility/debugger/reference/frameinfo.md)
- [IEnumDebugModules2](../../../extensibility/debugger/reference/ienumdebugmodules2.md)
