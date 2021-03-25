---
description: デバッグエンジン (DE) は、現在実行中のプログラムで例外がスローされた場合に、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。
title: IDebugExceptionEvent2 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 58a6b0beab4312b0622501e72a5d2c87ef84ccff
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105087874"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
デバッグエンジン (DE) は、現在実行中のプログラムで例外がスローされた場合に、このインターフェイスをセッションデバッグマネージャー (SDM) に送信します。

## <a name="syntax"></a>Syntax

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 DE は、デバッグ中のプログラムで例外が発生したことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は、 [QueryInterface](/cpp/atl/queryinterface) を使用してインターフェイスにアクセスし `IDebugEvent2` ます。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 DE は、このイベントオブジェクトを作成して送信し、例外を報告します。 イベントは、デバッグ対象のプログラムにアタッチされるときに SDM によって提供される [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md) callback 関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugExceptionEvent2` ます。

|メソッド|説明|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|このイベントを発生させた例外に関する詳細情報を取得します。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|このイベントを発生させた例外の、人間が判読できる説明を取得します。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|デバッグエンジン (DE) が、実行の再開時にデバッグ対象のプログラムにこの例外を渡すオプションをサポートするかどうかを決定します。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|例外を、実行の再開時にデバッグされるプログラムに渡すか、または例外を破棄する必要があるかを指定します。|

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="remarks"></a>注釈
 イベントを送信する前に、DE は、前に [setexception](../../../extensibility/debugger/reference/idebugengine2-setexception.md)を呼び出したことによって、この例外イベントが最初の機会または第2回の例外として指定されているかどうかを確認します。 初回例外として指定されている場合、 `IDebugExceptionEvent2` イベントは SDM に送信されます。 そうでない場合、DE は例外を処理する機会をアプリケーションに提供します。 例外ハンドラーが指定されておらず、例外が第2の例外として指定されている場合、 `IDebugExceptionEvent2` イベントは SDM に送信されます。 それ以外の場合、DE はプログラムの実行を再開し、オペレーティングシステムまたはランタイムは例外を処理します。

## <a name="see-also"></a>こちらもご覧ください
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
