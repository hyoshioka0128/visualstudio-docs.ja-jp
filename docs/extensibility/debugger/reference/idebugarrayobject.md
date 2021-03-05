---
description: このインターフェイスは、配列オブジェクトを表します。
title: IDebugArrayObject |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 16162cee8a02bf02b192336425101ec4bb579106
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158528"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターを実装するこの方法は非推奨とされます。 CLR 式エバリュエーターの実装の詳細については、「 [Clr 式](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators) エバリュエーターと [マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、配列オブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugArrayObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装側の注意
 式エバリュエーターは、配列を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)インターフェイスは、オブジェクトが配列を表す場合、 [QueryInterface](/cpp/atl/queryinterface)を使用してこのインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスのメソッドに加えて `IDebugObject` 、次のメソッドがインターフェイスに実装され `IDebugArrayObject` ます。

|メソッド|説明|
|------------|-----------------|
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|配列内の要素の数を取得します。|
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|配列の要素を取得します。|
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|配列のすべての要素を取得します。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|配列のランクを取得します。|
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|配列の次元を取得します。|

## <a name="remarks"></a>解説
 式エバリュエーターは、このインターフェイスを使用して、解析ツリー内の配列を表します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
