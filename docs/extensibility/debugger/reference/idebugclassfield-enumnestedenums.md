---
title: フィールド:列挙体 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedEnums
helpviewer_keywords:
- IDebugClassField::EnumNestedEnums method
ms.assetid: 90fd0cef-9145-4de6-91d4-6c881df39d6e
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 38ee3ccd1ffd3130bc918da18c631cf08683f064
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734409"
---
# <a name="idebugclassfieldenumnestedenums"></a>IDebugClassField::EnumNestedEnums
このクラスの入れ子になった列挙子の列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumNestedEnums(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedEnums(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
[アウト]入れ子になった列挙[体のリスト](../../../extensibility/debugger/reference/ienumdebugfields.md)を表すオブジェクトを返します。 入れ子になった列挙型がない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
正常に終了した場合は、S_OKを返すか、入れ子になった列挙子がない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
列挙体の各要素は、入れ子になった列挙体を記述する[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)オブジェクトです。

クラス内で宣言された列挙型は、入れ子になった列挙体と見なされます。 以下に例を示します。

```
class RootClass {
    enum NestedEnum { EnumValue = 0 }
};
```

この`EnumNestedEnums`メソッドは、列挙体を表す 1 つの[IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)オブジェクトを含む`NestedEnum`[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)オブジェクトを返します。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
