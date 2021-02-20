---
title: 'IDebugClassField:: EnumConstructors |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumConstructors
helpviewer_keywords:
- IDebugClassField::EnumConstructors method
ms.assetid: 66a250b2-75a0-45aa-8d58-40f91cc4bf7b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 05226572d7f1b708745887338c654674e71d0f5d
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99947083"
---
# <a name="idebugclassfieldenumconstructors"></a>IDebugClassField::EnumConstructors
このクラスのコンストラクターの列挙子を作成します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumConstructors( 
   CONSTRUCTOR_ENUM   cMatch,
   IEnumDebugFields** ppEnum
);
```

```csharp
int EnumConstructors(
   CONSTRUCTOR_ENUM     cMatch,
   out IEnumDebugFields ppEnum
);
```

## <a name="parameters"></a>パラメーター
`cMatch`\
から列挙するコンストラクターの型を指定する [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md) 列挙の値。

`ppEnum`\
入出力コンストラクターのリストを表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 コンストラクターが存在しない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK を返すか、コンストラクターが存在しない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>解説
 列挙体の各要素は、コンストラクターメソッドを記述する [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md) オブジェクトです。

 通常、コンストラクターの一覧には、コンパイラによって提供される既定のコンストラクターは含まれません。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)
