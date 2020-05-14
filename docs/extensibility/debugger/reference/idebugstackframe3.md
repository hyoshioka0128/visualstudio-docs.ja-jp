---
title: をクリックしてスタックフレーム 3 を実行する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugStackFrame3
helpviewer_keywords:
- IDebugStackFrame3 interface
ms.assetid: 39af2f57-0a01-42b8-b093-b7fbc61e2909
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: d86997d11e124fd5a47981314cf383f5cd8aff7d
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80719472"
---
# <a name="idebugstackframe3"></a>IDebugStackFrame3
このインターフェイスは、インターセプトされた例外を処理するために[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)を拡張します。

## <a name="syntax"></a>構文

```
IDebugStackFrame3 : IDebugStackFrame2
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 デバッグ エンジン (DE) は、インターセプトされた例外をサポートする[IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 この[QueryInterface](/cpp/atl/queryinterface)インターフェイスを取得するには`IDebugStackFrame2`、インターフェイスでクエリ インターフェイスを呼び出します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [から](../../../extensibility/debugger/reference/idebugstackframe2.md)継承されたメソッドに加えて、`IDebugStackFrame3`次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)|通常の例外処理の前に、現在のスタック フレームの例外を処理します。|
|[GetUnwindCodeContext](../../../extensibility/debugger/reference/idebugstackframe3-getunwindcodecontext.md)|スタック アンワインドが発生した場合は、コード コンテキストを返します。|

## <a name="remarks"></a>Remarks
 インターセプトされた例外は、デバッガーが例外を処理してから、通常の例外処理ルーチンがランタイムによって呼び出されることを意味します。 例外をインターセプトするということは、本来、例外ハンドラが存在しない場合でも、ランタイムが存在するふりをすることを意味します。

- [InterceptCurrentException](../../../extensibility/debugger/reference/idebugstackframe3-interceptcurrentexception.md)は、すべての通常の例外コールバック イベントの間に呼び出されます (唯一の例外は、混合モード コード (マネージ コードとアンマネージ コード) をデバッグしている場合です。 DE が実装`IDebugStackFrame3`しない場合、または DE が IDebugStackFrame3::`InterceptCurrentException` ( など`E_NOTIMPL`) からエラーを返す場合、デバッガーは例外を通常どおりに処理します。

 デバッガーは、例外をインターセプトすることで、デバッグ中のプログラムの状態を変更し、例外がスローされた時点で実行を再開できます。

> [!NOTE]
> インターセプトされた例外は、共通言語ランタイム (CLR) で実行されているプログラムのマネージ コードでのみ許可されます。

 デバッグ エンジンは、関数を使用して実行時に "metricExceptions" を値 1 に設定することで、例外の`SetMetric`インターセプトをサポートすることを示します。 詳細については、「 [SDK ヘルパーをデバッグする](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)」を参照してください。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [コア インターフェイス](../../../extensibility/debugger/reference/core-interfaces.md)
- [IDebugStackFrame2](../../../extensibility/debugger/reference/idebugstackframe2.md)
- [デバッグ用の SDK ヘルパー](../../../extensibility/debugger/reference/sdk-helpers-for-debugging.md)
