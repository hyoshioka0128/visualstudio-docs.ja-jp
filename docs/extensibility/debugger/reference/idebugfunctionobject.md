---
title: IDebugFunctionObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugFunctionObject
helpviewer_keywords:
- IDebugFunctionObject interface
ms.assetid: 8d94e97c-a9d1-400c-8a98-a44b5385b33a
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 6433c1f2c540b040a3b3beccc264377e69592387
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80728489"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、関数を表します。

## <a name="syntax"></a>構文

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、このインターフェイスを実装して関数を表します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 このインターフェイスは、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) インターフェイスを特殊化したものであり、インターフェイスの [QueryInterface](/cpp/atl/queryinterface) を使用して取得され `IDebugObject` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスは、 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)から継承されたメソッドに加えて、 `IDebugFunctionObject` 次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|プリミティブデータオブジェクトを作成します。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|コンストラクターを使用してオブジェクトを作成します。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|コンストラクターを持たないオブジェクトを作成します。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|配列オブジェクトを作成します。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|文字列オブジェクトを作成します。|
|[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|関数を呼び出し、結果の値をオブジェクトとして返します。|

## <a name="remarks"></a>解説
 このインターフェイスは、式エバリュエーターが解析ツリー内の関数を表すことができるようにします。 `Create`このインターフェイスのメソッドは、メソッドに対する入力パラメーターを表すオブジェクトを構築するために使用されます。 関数は、関数の戻り値を表すオブジェクトを返す [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) メソッドを呼び出すことによって実行できます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
