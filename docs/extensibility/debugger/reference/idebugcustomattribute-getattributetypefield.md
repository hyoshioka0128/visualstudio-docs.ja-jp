---
title: 'IDebugCustomAttribute:: GetAttributeTypeField |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeTypeField
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeTypeField
ms.assetid: d6ce26d5-42ba-44c1-8659-0516db5bc82d
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3fa72b6dfc02f29e5efd8d3e04f98f078cba66a2
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99928446"
---
# <a name="idebugcustomattributegetattributetypefield"></a>IDebugCustomAttribute::GetAttributeTypeField
カスタム属性クラスの型を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAttributeTypeField( 
   IDebugClassField** ppCAType
);
```

```csharp
int GetAttributeTypeField(
   out IDebugClassField ppCAType
);
```

## <a name="parameters"></a>パラメーター
`ppCAType`\
入出力カスタム属性がインスタンスであるクラスを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 カスタム属性は常にクラスです。 このメソッドは、そのクラスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトへのアクセスを提供します。

## <a name="see-also"></a>関連項目
- [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)
- [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
