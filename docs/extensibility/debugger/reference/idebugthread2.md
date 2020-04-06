---
title: をクリックします。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 1965ff1b4cfa89e4584c194942dec7ae486473ff
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80718583"
---
# <a name="idebugthread2"></a>IDebugThread2
このインターフェイスは、プログラムで実行されているスレッドを表します。

## <a name="syntax"></a>構文

```
IDebugThread2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、単一のプログラムで実行スレッドを表すこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)を呼び出して、現在アクティブなスレッドを表すこのインターフェイスを取得します。

 このインターフェイスは、ブレークポイント要求の作成にも使用されます[(BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)を参照)。

 このインターフェイスは、バインドまたはエラーのブレークポイントを解決するときにも返されます[(BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)と[BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)を参照)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugThread2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|このスレッドのスタック フレームの一覧を取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|スレッドの名前を取得します。|
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|スレッドの名前を設定します。|
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|スレッドが実行されているプログラムを取得します。|
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|次のステートメントを、指定されたスタック フレームとコード コンテキストに設定できるかどうかを判断します。|
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|次のステートメントを、指定されたスタック フレームとコード コンテキストに設定します。|
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|システム スレッド識別子を取得します。|
|[中断](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|スレッドを中断します。|
|[Resume](../../../extensibility/debugger/reference/idebugthread2-resume.md)|スレッドを再開します。|
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|スレッドを記述するプロパティを取得します。|
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|この物理スレッドに関連付けられている論理スレッドを取得します。|

## <a name="remarks"></a>Remarks
 1 つの物理スレッドは複数のプログラムで実行できるため、複数`IDebugThread2`のプログラムから複数の物理スレッドを表すことができます。

 ブレークポイントまたは例外が発生すると[、Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)を呼び出してイベントが送信されます。 このメソッドの引数の 1 つは`IDebugThread2`、現在のスレッドを表すインターフェイスです。 現在[の](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)スタック フレームの[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスを取得するために使用されます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
