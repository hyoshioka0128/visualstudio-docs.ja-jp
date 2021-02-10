---
title: IDebugStackFrame3 |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 5511624fb69015351d8cc37d6b27ad142a5956d4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99961184"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
このインターフェイスは、インターセプトされた例外を処理するために [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) を拡張します。

## <a name="syntax"></a>構文

```
IDebugStackFrame3 : IDebugStackFrame2
```

## <a name="notes-for-implementers"></a>実装側の注意
 デバッグエンジン (DE) は、インターセプトされた例外をサポートするために、 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を呼び出して、 `IDebugStackFrame2` このインターフェイスを取得します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)から継承されたメソッドに加えて、は `IDebugStackFrame3` 次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|通常の例外処理の前に、現在のスタックフレームの例外を処理します。|
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|スタックアンワインドが発生した場合は、コードコンテキストを返します。|

## <a name="remarks"></a>解説
 インターセプトされた例外は、通常の例外処理ルーチンが実行時に呼び出される前に、デバッガーが例外を処理できることを意味します。 例外をインターセプトすることは、基本的に、実行時に例外ハンドラーが存在しないということを示しています。

- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md) は、通常のすべての例外コールバックイベントの発生時に呼び出されます (唯一の例外は、混合モードコード (マネージコードとアンマネージコード) をデバッグする場合です。この場合、最後のコールバック時に例外を受け取ることはできません)。 DE がを実装していない場合、 `IDebugStackFrame3` または de によって IDebugStackFrame3:: (など) からエラーが返された場合、 `InterceptCurrentException` `E_NOTIMPL` デバッガーは通常どおり例外を処理します。

 デバッガーでは、例外を受け取ることにより、デバッグ中のプログラムの状態を変更して、例外がスローされた時点で実行を再開できるようにすることができます。

> [!NOTE]
> インターセプトされた例外は、マネージコード、つまり共通言語ランタイム (CLR) で実行されているプログラムでのみ使用できます。

 デバッグエンジンは、関数を使用して、実行時に "metricExceptions" を1の値に設定することによって、例外のインターセプトをサポートしていることを示してい `SetMetric` ます。 詳細については、「 [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)」を参照してください。

## <a name="requirements"></a>要件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [コアインターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
