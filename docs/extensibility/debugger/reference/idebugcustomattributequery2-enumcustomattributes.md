---
title: 'IDebugCustomAttributeQuery2:: EnumCustomAttributes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
helpviewer_keywords:
- IDebugCustomAttributeQuery2::EnumCustomAttributes
ms.assetid: 94bfce74-aa3d-45f0-8e04-5715faf85217
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 97476647c42dc66d3998aecf2c717fa3bbb08cf4
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99842460"
---
# <a name="idebugcustomattributequery2enumcustomattributes"></a>IDebugCustomAttributeQuery2::EnumCustomAttributes
このフィールドにアタッチされているすべてのカスタム属性の列挙子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT EnumCustomAttributes( 
   IEnumDebugCustomAttributes** ppEnum
);
```

```csharp
int EnumCustomAttributes(
   out IEnumDebugCustomAttributes ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力カスタム属性の一覧を表す [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md) オブジェクトを返します。それ以外の場合、カスタム属性がない場合、は null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合、このフィールドにカスタム属性がない場合は S_OK または S_FALSE を返します。 それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 フィールドは、複数のカスタム属性を持つことができます。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
- [IEnumDebugCustomAttributes](../../../extensibility/debugger/reference/ienumdebugcustomattributes.md)
