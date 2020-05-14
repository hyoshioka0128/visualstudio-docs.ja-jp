---
title: プロパティを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetBackingFieldForProperty
helpviewer_keywords:
- IDebugObject2::GetBackingFieldForProperty method
ms.assetid: e72c6338-5573-4fad-8075-f3ade3435424
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: b5b9fed9b071f34c119c8e4a5af12c1df7990f4c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726245"
---
# <a name="idebugobject2getbackingfieldforproperty"></a>IDebugObject2::GetBackingFieldForProperty
このオブジェクトによって表されるプロパティをバッキングしている可能性があるフィールドまたは変数 (存在する場合) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBackingFieldForProperty(
   IDebugObject2** ppObject
);
```

```csharp
int GetBackingFieldForProperty(
   out IDebugObject2 ppObject
);
```

## <a name="parameters"></a>パラメーター
`ppObject`\
[アウト]バッキング フィールドを記述する[IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)オブジェクト。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)オブジェクトは、マネージ コード クラスプロパティ、つまり get アクセサーまたは set アクセサーを持つメソッドを表します。 このようなプロパティは、通常、プロパティによって操作される値を格納する変数を必要とします。 この変数はバッキングフィールドと呼ばれます。 オブジェクトのバッキング フィールドがない場合は、null 値を返すようにしてください。 `ppObject`

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
