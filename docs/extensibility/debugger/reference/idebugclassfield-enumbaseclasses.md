---
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 12317c549050be31ac9e19bc7b3d8a6683f743d0
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80734472"
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
