---
title: を定義します。マイクロソフトドキュメント
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
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
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
[in]検索するカスタム属性の名前を含む文字列。

## <a name="return-value"></a>戻り値
 このフィールドにカスタム属性が定義されている場合はS_OKを返し、それ以外の場合はS_FALSEを返します。

## <a name="remarks"></a>Remarks
 カスタム属性に関連付けられた属性バイトを取得するには[、メソッドを](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md)呼び出します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
