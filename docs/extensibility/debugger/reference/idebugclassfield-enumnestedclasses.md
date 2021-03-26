---
description: このクラスで入れ子になっているクラスの列挙子を作成します。
title: 'IDebugClassField:: EnumNestedClasses |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumNestedClasses
helpviewer_keywords:
- IDebugClassField::EnumNestedClasses method
ms.assetid: 2ba5ef0c-395e-4006-9e3c-9b06e1d711d0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 95f423b556263dc7ad634feaebda90d62eeeeb04
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105088576"
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

## <a name="remarks"></a>注釈
列挙体の各要素は、入れ子になったクラスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。

入れ子になったクラスは、別のクラス内で定義されたクラスです。 次に例を示します。

```
class RootClass {
   class NestedClass { }
};
```

[IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)列挙体には、クラスを表す1つのオブジェクトが含まれ `NestedClass` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
