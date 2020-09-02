---
title: 'IDebugClassField:: EnumNestedClasses |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3e6ef918b55d8b311380264d688085b0d2803601
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734439"
---
# <a name="idebugclassfieldenumnestedclasses"></a>IDebugClassField::EnumNestedClasses
このクラスで入れ子になっているクラスの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumNestedClasses(
    IEnumDebugFields** ppEnum
);
```

```csharp
int EnumNestedClasses(
    out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力入れ子になったクラスのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 入れ子になったクラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
成功した場合は、S_OK を返すか、入れ子になったクラスがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
列挙体の各要素は、入れ子になったクラスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。

入れ子になったクラスは、別のクラス内で定義されたクラスです。 次に例を示します。

```
class RootClass {
   class NestedClass { }
};
```

[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)列挙体には、クラスを表す1つのオブジェクトが含まれ `NestedClass` ます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
