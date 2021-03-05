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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 2d5ef86e5f4fea89b376404703000c8bd7e861a0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150719"
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

## <a name="remarks"></a>解説
 列挙子オブジェクトの基底クラスは、最も直接的な (または最も派生した) 基底クラスから最もリモートの基底クラスまで、順に指定されます。 たとえば、次の C++ クラスがあるとします。

```
class Root { }
class Level1 : Root { }
class Level2 : Level1 { }
class MyClass : Level2 { }
```

 列挙型では、基本クラスが、、の順に返され `Level2` `Level1` `Root` ます。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
