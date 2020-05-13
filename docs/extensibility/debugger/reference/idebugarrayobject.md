---
title: オブジェクトを返す |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject
helpviewer_keywords:
- IDebugArrayObject method
ms.assetid: a1c8e77e-dee1-4748-a516-6ab032a8f54f
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 709273b89d89759163acb725220d1092d33ad72f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736214"
---
# <a name="idebugarrayobject"></a>IDebugArrayObject
> [!IMPORTANT]
> Visual Studio 2015 では、式エバリュエーターのこの実装方法は非推奨になりました。 CLR 式エバリュエーターの実装については、「 [CLR 式エバリュエーター](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/CLR-Expression-Evaluators)と[マネージ式エバリュエーターのサンプル](https://github.com/Microsoft/ConcordExtensibilitySamples/wiki/Managed-Expression-Evaluator-Sample)」を参照してください。

 このインターフェイスは、配列オブジェクトを表します。

## <a name="syntax"></a>構文

```
IDebugArrayObject : IDebugObject
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 式エバリュエーターは、配列を表すためにこのインターフェイスを実装します。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [インターフェイス](../../../extensibility/debugger/reference/idebugobject.md)は、オブジェクトが配列を表す場合は[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用して、このインターフェイスを取得できます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 `IDebugObject`インターフェイスのメソッドに加えて、次のメソッドが`IDebugArrayObject`インターフェイスに実装されます。

|Method|説明|
|------------|-----------------|
|[GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md)|配列内の要素の数を取得します。|
|[GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)|配列の要素を取得します。|
|[GetElements](../../../extensibility/debugger/reference/idebugarrayobject-getelements.md)|配列のすべての要素を取得します。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayobject-getrank.md)|配列のランクを取得します。|
|[GetDimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)|配列の次元を取得します。|

## <a name="remarks"></a>Remarks
 式エバリュエーターは、このインターフェイスを使用して解析ツリー内の配列を表します。

## <a name="requirements"></a>必要条件
 ヘッダー: ee.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
