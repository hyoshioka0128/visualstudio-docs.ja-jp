---
title: プロパティフィールド |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPropertyField
helpviewer_keywords:
- IDebugPropertyField interface
ms.assetid: b50edb2c-fb8d-4def-993d-17d23d2027c1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
ms.openlocfilehash: 96a3f3c2dca16cd2c28c9d1727e4ac145c91c482
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80720698"
---
# <a name="idebugpropertyfield"></a>IDebugPropertyField
このインターフェイスは、プロパティの取得と設定を可能にする関数を提供します。

## <a name="syntax"></a>構文

```
IDebugPropertyField : IDebugContainerField
```

## <a name="notes-for-implementers"></a>実装者向けの注意事項
 シンボル プロバイダーは、[この](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスを実装する同じオブジェクトに実装します。 このインターフェイスは、クラスのプロパティの概念をサポートする特殊化です。

## <a name="notes-for-callers"></a>発信者向けのメモ
 [メソッド](../../../extensibility/debugger/reference/idebugfield-getkind.md)が返`FIELD_KIND_PROP`す[場合は、](../../../extensibility/debugger/reference/idebugcontainerfield.md)インターフェイスからこのインターフェイスを取得するのには[、クエリ インターフェイス](/cpp/atl/queryinterface)を使用します。

## <a name="methods-in-vtable-order"></a>Vtable 順序のメソッド
 インターフェイスのメソッドに加えて、[IDebugField](../../../extensibility/debugger/reference/idebugfield.md)[このインターフェイスは](../../../extensibility/debugger/reference/idebugcontainerfield.md)、次のメソッドを実装します。

|Method|説明|
|------------|-----------------|
|[GetPropertyGetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertygetter.md)|プロパティを取得するメソッドを取得します。|
|[GetPropertySetter](../../../extensibility/debugger/reference/idebugpropertyfield-getpropertysetter.md)|プロパティを設定するメソッドを取得します。|

## <a name="remarks"></a>Remarks
 プロパティはマネージ コードの概念であり、変数として扱われるメソッドを表します。 アンマネージ C++ にはプロパティが存在しません。

## <a name="requirements"></a>必要条件
 ヘッダー: sh.h

 名前空間: を使用します。

 アセンブリ:

## <a name="see-also"></a>関連項目
- [シンボル プロバイダーのインターフェイス](../../../extensibility/debugger/reference/symbol-provider-interfaces.md)
- [IDebugContainerField](../../../extensibility/debugger/reference/idebugcontainerfield.md)
