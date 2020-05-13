---
title: イベントイベント2マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugExceptionEvent2
helpviewer_keywords:
- IDebugExceptionEvent2 interface
ms.assetid: 53d32e59-a84b-4710-833e-c5ab08100516
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: cbd53d56b21886e972b33c219367edd603cbf0d5
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80729782"
---
# <a name="idebugexceptionevent2"></a>IDebugExceptionEvent2
デバッグ エンジン (DE) は、現在実行されているプログラムで例外がスローされたときに、セッション デバッグ マネージャー (SDM) にこのインターフェイスを送信します。

## <a name="syntax"></a>構文

```
IDebugExceptionEvent2 : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 DE は、デバッグ中のプログラムで例外が発生したことを報告するために、このインターフェイスを実装します。 [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)インターフェイスは、このインターフェイスと同じオブジェクトに実装する必要があります。 SDM は[、インターフェイス](/cpp/atl/queryinterface)にアクセスするのに`IDebugEvent2`クエリ インターフェイスを使用します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 DE は、このイベント オブジェクトを作成して送信し、例外を報告します。 イベントは、デバッグ中のプログラムにアタッチされたときに SDM によって提供される[IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)コールバック関数を使用して送信されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugExceptionEvent2`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[GetException](../../../extensibility/debugger/reference/idebugexceptionevent2-getexception.md)|このイベントを発生した例外に関する詳細情報を取得します。|
|[GetExceptionDescription](../../../extensibility/debugger/reference/idebugexceptionevent2-getexceptiondescription.md)|このイベントを発生した例外の、人間が判読できる説明を取得します。|
|[CanPassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-canpasstodebuggee.md)|デバッグ エンジン (DE) が、実行が再開されたときにデバッグ中のプログラムにこの例外を渡すオプションをサポートするかどうかを決定します。|
|[PassToDebuggee](../../../extensibility/debugger/reference/idebugexceptionevent2-passtodebuggee.md)|実行が再開されるときに、デバッグ中のプログラムに例外を渡すか、または例外を破棄するかを指定します。|

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="remarks"></a>Remarks
 イベントを送信する前に、DE は、この例外イベントが[SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)への以前の呼び出しによって初回または 2 番目のチャンスの例外に指定されているかどうかを確認します。 初回例外として指定されている場合、`IDebugExceptionEvent2`イベントは SDM に送信されます。 ない場合、DE は、アプリケーションに例外を処理する機会を与えます。 例外ハンドラーが指定されていない場合、例外が 2 次例外として指定されている場合、`IDebugExceptionEvent2`イベントは SDM に送信されます。 それ以外の場合、DE はプログラムの実行を再開し、オペレーティング システムまたはランタイムが例外を処理します。

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [SetException](../../../extensibility/debugger/reference/idebugengine2-setexception.md)
- [IDebugEvent2](../../../extensibility/debugger/reference/idebugevent2.md)
- [IDebugEventCallback2](../../../extensibility/debugger/reference/idebugeventcallback2.md)
