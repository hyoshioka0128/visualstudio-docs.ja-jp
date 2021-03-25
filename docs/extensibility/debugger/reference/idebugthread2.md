---
description: このインターフェイスは、プログラムで実行されているスレッドを表します。
title: IDebugThread2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugThread2
helpviewer_keywords:
- IDebugThread2 interface
ms.assetid: 221b4b1b-4a26-466e-bc29-5eff800fab13
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 24a9cef2e62dc2597871f270c9ee48ad58c0a0e1
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105086977"
---
# <a name="idebugthread2"></a>IDebugThread2
このインターフェイスは、プログラムで実行されているスレッドを表します。

## <a name="syntax"></a>Syntax

```
IDebugThread2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、1つのプログラムでの実行スレッドを表すために、このインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getthread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)を呼び出して、現在アクティブなスレッドを表すこのインターフェイスを取得します。

 このインターフェイスは、ブレークポイント要求の作成にも使用されます ( [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)を参照してください)。

 このインターフェイスは、バインドまたはエラーのブレークポイントを解決するときにも返されます ( [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md) と [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)を参照してください)。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugThread2` ます。

|メソッド|説明|
|------------|-----------------|
|[EnumFrameInfo](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md)|このスレッドのスタックフレームの一覧を取得します。|
|[GetName](../../../extensibility/debugger/reference/idebugthread2-getname.md)|スレッドの名前を取得します。|
|[SetThreadName](../../../extensibility/debugger/reference/idebugthread2-setthreadname.md)|スレッドの名前を設定します。|
|[GetProgram](../../../extensibility/debugger/reference/idebugthread2-getprogram.md)|スレッドが実行されているプログラムを取得します。|
|[CanSetNextStatement](../../../extensibility/debugger/reference/idebugthread2-cansetnextstatement.md)|次のステートメントを指定したスタックフレームとコードコンテキストに設定できるかどうかを判断します。|
|[SetNextStatement](../../../extensibility/debugger/reference/idebugthread2-setnextstatement.md)|指定されたスタックフレームおよびコードコンテキストに次のステートメントを設定します。|
|[GetThreadId](../../../extensibility/debugger/reference/idebugthread2-getthreadid.md)|システムスレッド識別子を取得します。|
|[[中断]](../../../extensibility/debugger/reference/idebugthread2-suspend.md)|スレッドを中断します。|
|[再開](../../../extensibility/debugger/reference/idebugthread2-resume.md)|スレッドを再開します。|
|[GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)|スレッドを説明するプロパティを取得します。|
|[GetLogicalThread](../../../extensibility/debugger/reference/idebugthread2-getlogicalthread.md)|この物理スレッドに関連付けられている論理スレッドを取得します。|

## <a name="remarks"></a>注釈
 1つの物理スレッドが複数のプログラムで実行される可能性があるため、複数の `IDebugThread2` プログラムから複数のプログラムが同じ物理スレッドを表すことができます。

 ブレークポイントまたは例外が発生した場合、イベントは呼び出し元の [イベント](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)によって送信されます。 このメソッドの引数の1つは、 `IDebugThread2` 現在のスレッドを表すインターフェイスです。 [Enumframe info](../../../extensibility/debugger/reference/idebugthread2-enumframeinfo.md) は、現在のスタックフレームの [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスを取得するために使用されます。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [Event](../../../extensibility/debugger/reference/idebugeventcallback2-event.md)
- [GetThread](../../../extensibility/debugger/reference/idebugstackframe2-getthread.md)
- [BP_REQUEST_INFO](../../../extensibility/debugger/reference/bp-request-info.md)
- [BP_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-resolution-info.md)
- [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)
