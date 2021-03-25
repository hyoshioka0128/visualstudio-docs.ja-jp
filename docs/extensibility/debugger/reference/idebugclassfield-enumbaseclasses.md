---
description: このクラスの基本クラスの列挙子を作成します。
title: 'IDebugClassField:: EnumBaseClasses |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumBaseClasses
helpviewer_keywords:
- IDebugClassField::EnumBaseClasses method
ms.assetid: 78749674-ef75-46d3-a1f4-ff33afd90e32
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9ba31ead00ad2312b66273a2ddfaeebd252e0981
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105084988"
---
# <a name="idebugclassfieldenumbaseclasses"></a>IDebugClassField::EnumBaseClasses
このクラスの基本クラスの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumBaseClasses( 
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumBaseClasses(
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\

入出力基底クラスのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 基底クラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 正常に終了した場合は S_OK を返し、基本クラスがない場合は S_SH_NO_BASE_CLASSES を返します ( `ppEnum` パラメーターが null 値に設定されている場合)。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 列挙子オブジェクトの基底クラスは、最も直接的な (または最も派生した) 基底クラスから最もリモートの基底クラスまで、順に指定されます。 たとえば、次の C++ クラスがあるとします。

```
class Root { }
class Level1 : Root { }
class Level2 : Level1 { }
class MyClass : Level2 { }
```

 列挙型では、基本クラスが、、の順に返され `Level2` `Level1` `Root` ます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
