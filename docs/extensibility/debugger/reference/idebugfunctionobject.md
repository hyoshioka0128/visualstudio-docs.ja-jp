---
title: オブジェクト |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80728489"
---
# <a name="idebugfunctionobject"></a>IDebugFunctionObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは関数を表します。

## <a name="syntax"></a>構文

```
IDebugFunctionObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、関数を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 このインターフェイスは[、IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスの特殊化であり、インターフェイスで[クエリ インターフェイス](/cpp/atl/queryinterface)を`IDebugObject`使用して取得されます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 [から](../../../extensibility/debugger/reference/idebugobject.md)継承されたメソッドに加えて、インターフェイスは`IDebugFunctionObject`、次のメソッドを公開します。

|Method|説明|
|------------|-----------------|
|[CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)|プリミティブ データ オブジェクトを作成します。|
|[CreateObject](../../../extensibility/debugger/reference/idebugfunctionobject-createobject.md)|コンストラクターを使用してオブジェクトを作成します。|
|[CreateObjectNoConstructor](../../../extensibility/debugger/reference/idebugfunctionobject-createobjectnoconstructor.md)|コンストラクターを持たないオブジェクトを作成します。|
|[CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)|配列オブジェクトを作成します。|
|[CreateStringObject](../../../extensibility/debugger/reference/idebugfunctionobject-createstringobject.md)|文字列オブジェクトを作成します。|
|[評価](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)|関数を呼び出し、結果の値をオブジェクトとして返します。|

## <a name="remarks"></a>Remarks
 このインターフェイスを使用すると、式エバリュエーターは解析ツリー内の関数を表すことができます。 この`Create`インターフェイスのメソッドは、メソッドへの入力パラメータを表すオブジェクトを構築するために使用されます。 この関数は、関数の戻り値を表すオブジェクトを返す[Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md)メソッドを呼び出すことによって実行できます。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [式の評価のインターフェイス](../../../extensibility/debugger/reference/expression-evaluation-interfaces.md)
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
