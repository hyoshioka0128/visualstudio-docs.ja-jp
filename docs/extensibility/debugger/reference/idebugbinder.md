---
title: Iデバッグバインダー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder
helpviewer_keywords:
- IDebugBinder interface
ms.assetid: d1f31e5b-c6e2-4e02-8959-b3e86041b29c
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: fcdec19c4667356edaf9e057c86ddc24baf747b7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80735970"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、シンボル の現在の値を含むメモリ コンテキストまたはオブジェクトに、シンボル プロバイダーによって返されるシンボル フィールドをバインドします。

## <a name="syntax"></a>構文

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 このインターフェイスは、式の評価をサポートし、デバッグ エンジン (DE) によって実装する必要があります。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは式の評価のプロセスで使用され、通常は[EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)および[EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)の実装で使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に`IDebugBinder`、 のメソッドを示します。

|Method|説明|
|------------|-----------------|
|[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)|シンボルの現在の値を格納しているメモリ コンテキストまたはオブジェクトを取得します。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|オブジェクトの実行時の型を決定します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|オブジェクトの場所またはメモリ アドレスをメモリ コンテキストに変換します。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|関数パラメーター[の作成](../../../extensibility/debugger/reference/idebugfunctionobject.md)に使用されるオブジェクトを取得します。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|変数の正確な型を取得します。|

## <a name="remarks"></a>Remarks
 このインターフェイスは、解析ツリー内の式エバリュエーターによって使用されるオブジェクトを返します。 式エバリュエーターは、シンボル プロバイダーを使用して式を解析し、式のシンボルを[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)のインスタンスに変換します。 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)メソッドは、`IDebugField`シンボル型をメモリ内の実際の値に接続またはバインドするオブジェクトを[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトに変換します。 これらの`IDebugObject`オブジェクトは、後で評価するために解析ツリーに格納されます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
