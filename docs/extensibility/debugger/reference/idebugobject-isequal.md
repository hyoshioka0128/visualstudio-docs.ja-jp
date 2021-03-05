---
description: オブジェクトとこのオブジェクトを比較します。
title: 'IDebugObject:: IsEqual |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 0907b72f2a0647fc6ff6181ecdc5c7fd8c2134cb
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102151663"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
オブジェクトとこのオブジェクトを比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT IsEqual( 
   IDebugObject* pObject,
   BOOL*         pfIsEqual
);
```

```csharp
int IsEqual(
   IDebugObject pObject,
   out int      pfIsEqual
);
```

## <a name="parameters"></a>パラメーター
`pObject`\
からと比較するオブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト。

`pfIsEqual`\
入出力`TRUE`オブジェクトの値が等しい場合は0以外 () を返します。それ以外の場合は 0 () を返し `FALSE` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 通常、このメソッドは、パラメーターとこの IDebugObject オブジェクトによって表される値のアドレスを比較できます `pObject` 。アドレスが等しい場合は、それらのオブジェクトが等しいと見なされます。 [](../../../extensibility/debugger/reference/idebugobject.md)

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
