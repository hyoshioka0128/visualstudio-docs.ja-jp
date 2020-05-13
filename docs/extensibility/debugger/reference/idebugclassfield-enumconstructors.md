---
title: '列挙型フィールド: 列挙型 |マイクロソフトドキュメント'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumConstructors
helpviewer_keywords:
- IDebugClassField::EnumConstructors method
ms.assetid: 66a250b2-75a0-45aa-8d58-40f91cc4bf7b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 607f4f4af3021389628fcc1be446ebbe95628b7c
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80734456"
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
[in]列挙体のコンストラクターの型を指定する[CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)列挙体の値。

`ppEnum`\
[アウト]コンストラクターの[一](../../../extensibility/debugger/reference/ienumdebugfields.md)覧を表すオブジェクトを返します。 コンストラクターがない場合は、null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OKを返すか、コンストラクターがない場合はS_FALSEを返します。 それ以外の場合はエラー コードを返します。

## <a name="remarks"></a>Remarks
 列挙体の各要素は、コンストラクター メソッドを記述する[IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)オブジェクトです。

 通常、コンストラクターのリストには、コンパイラによって提供される既定のコンストラクターは含まれません。

## <a name="see-also"></a>関連項目
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
- [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
- [IDebugMethodField](../../../extensibility/debugger/reference/idebugmethodfield.md)
- [CONSTRUCTOR_ENUM](../../../extensibility/debugger/reference/constructor-enum.md)
