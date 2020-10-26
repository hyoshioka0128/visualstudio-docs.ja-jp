---
title: 'IDebugCustomAttributeQuery2:: IsCustomAttributeDefined |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
helpviewer_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
ms.assetid: 5c07cc52-6d2d-42df-9d76-9f1f769641db
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 7be649a5d65f88d8263bbe8950fda1a157855ed2
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80732537"
---
# <a name="idebugcustomattributequery2iscustomattributedefined"></a>IDebugCustomAttributeQuery2::IsCustomAttributeDefined
カスタム属性が名前によって存在するかどうかを判断します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsCustomAttributeDefined( 
   LPCOLESTR pszCustomAttributeName
);
```

```csharp
int IsCustomAttributeDefined(
   [In] string pszCustomAttributeName
);
```

## <a name="parameters"></a>パラメーター
`pszCustomAttributeName`\
から検索するカスタム属性の名前を格納している文字列。

## <a name="return-value"></a>戻り値
 このフィールドにカスタム属性が定義されている場合は S_OK を返し、それ以外の場合は S_FALSE を返します。

## <a name="remarks"></a>解説
 カスタム属性に関連付けられている属性のバイト数を取得するには、 [GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md) メソッドを呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
