---
title: IDebugBinder |Microsoft Docs
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
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80735970"
---
# <a name="idebugbinder"></a>IDebugBinder
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、通常、シンボルプロバイダーによって返されるシンボルフィールドを、シンボルの現在の値を含むメモリコンテキストまたはオブジェクトにバインドします。

## <a name="syntax"></a>構文

```
IDebugBinder : IUnknown
```

## <a name="notes-for-implementers"></a>実装側の注意
 このインターフェイスは、式の評価をサポートし、デバッグエンジン (DE) によって実装される必要があります。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、式の評価プロセスで使用され、通常は [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md) および [evaluateasync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)の実装で使用されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 次の表に、のメソッドを示し `IDebugBinder` ます。

|Method|説明|
|------------|-----------------|
|[Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)|シンボルの現在の値を格納しているメモリコンテキストまたはオブジェクトを取得します。|
|[ResolveRuntimeType](../../../extensibility/debugger/reference/idebugbinder-resolveruntimetype.md)|オブジェクトの実行時の型を決定します。|
|[GetMemoryContext](../../../extensibility/debugger/reference/idebugbinder-getmemorycontext.md)|オブジェクトの場所またはメモリアドレスをメモリコンテキストに変換します。|
|[GetFunctionObject](../../../extensibility/debugger/reference/idebugbinder-getfunctionobject.md)|関数パラメーターの作成に使用される [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md) オブジェクトを取得します。|
|[ResolveDynamicType](../../../extensibility/debugger/reference/idebugbinder-resolvedynamictype.md)|変数の正確な型を取得します。|

## <a name="remarks"></a>解説
 このインターフェイスは、解析ツリーの式エバリュエーターによって使用されるオブジェクトを返します。 式エバリュエーターは、シンボルプロバイダーを使用して式を解析し、式のシンボルを [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)のインスタンスに変換します。これにより、ソースコード内の型と場所について、各シンボルが記述されます。 [Bind](../../../extensibility/debugger/reference/idebugbinder-bind.md)メソッドは、 `IDebugField` オブジェクトを[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトに変換します。このオブジェクトは、シンボル型をメモリ内の実際の値に接続またはバインドします。 これらの `IDebugObject` オブジェクトは、後で評価できるように解析ツリーに格納されます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [EvaluateSync](../../../extensibility/debugger/reference/idebugexpression2-evaluatesync.md)
- [EvaluateAsync](../../../extensibility/debugger/reference/idebugexpression2-evaluateasync.md)
- [IDebugFunctionObject](../../../extensibility/debugger/reference/idebugfunctionobject.md)
