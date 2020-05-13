---
title: クラスフィールド::列挙クラス |マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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

[アウト]基本クラス[のリスト](../../../extensibility/debugger/reference/ienumdebugfields.md)を表すオブジェクトを返します。 基本クラスがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返し、基底クラスがない場合はS_SH_NO_BASE_CLASSES`ppEnum`を返します (パラメーターが null 値に設定されている場合)。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 列挙子オブジェクトの基底クラスは、最も直接的な (または最も派生した) 基底クラスの順序で最もリモートの基底クラスに指定されます。 たとえば、C++ クラスを指定します。

```
class Root { }
class Level1 : Root { }
class Level2 : Level1 { }
class MyClass : Level2 { }
```

 列挙体は、基本クラスを 、 `Level2`、`Level1`という`Root`順序で返します。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
