---
description: このインターフェイスは、配列のシンボルまたは型を表します。
title: IDebugArrayField |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: b3926bb47e1ea8a91289a7454f289cd3806e97f7
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158723"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
このインターフェイスは、配列のシンボルまたは型を表します。

## <a name="syntax"></a>構文

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装側の注意
 シンボルプロバイダーは、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、配列オブジェクトを表す特殊化です。

## <a name="notes-for-callers"></a>呼び出し元に関する注意事項
 [Getkind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がフラグを返す場合は、 [QueryInterface](/cpp/atl/queryinterface)を使用して、 [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスからこのインターフェイスを取得し `FIELD_TYPE_ARRAY` ます。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 このインターフェイスは、 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) インターフェイスと [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md) インターフェイスのメソッドに加えて、次のものを実装します。

|メソッド|説明|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|配列内の要素の数を取得します。|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|配列内の要素の型を取得します。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|配列のランクを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
