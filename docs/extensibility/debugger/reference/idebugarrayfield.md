---
title: を指定する |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField
helpviewer_keywords:
- IDebugArrayField interface
ms.assetid: 9667b0a5-4295-46cc-9388-b75c1350be15
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: dab01c1e956ced7e6894b951ab16f4ce68eb778b
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736294"
---
# <a name="idebugarrayfield"></a>IDebugArrayField
このインターフェイスは、配列のシンボルまたは型を記述します。

## <a name="syntax"></a>構文

```
IDebugArrayField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは[、IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスを実装する同じオブジェクトにこのインターフェイスを実装します。 このインターフェイスは、配列オブジェクトを表す特殊化です。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [GetKind](../../../extensibility/debugger/reference/idebugfield-getkind.md)がフラグ`FIELD_TYPE_ARRAY`を[返す場合](../../../extensibility/debugger/reference/idebugcontainerfield.md)は、インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスのメソッドに加えて、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)[このインターフェイスは](../../../extensibility/debugger/reference/idebugcontainerfield.md)、次を実装します。

|Method|説明|
|------------|-----------------|
|[GetNumberOfElements](../../../extensibility/debugger/reference/idebugarrayfield-getnumberofelements.md)|配列内の要素の数を取得します。|
|[GetElementType](../../../extensibility/debugger/reference/idebugarrayfield-getelementtype.md)|配列内の要素の型を取得します。|
|[GetRank](../../../extensibility/debugger/reference/idebugarrayfield-getrank.md)|配列のランクを取得します。|

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
