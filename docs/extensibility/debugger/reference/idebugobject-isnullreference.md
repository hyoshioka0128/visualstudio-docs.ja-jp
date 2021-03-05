---
description: このオブジェクトが null 参照であるかどうかをテストします。
title: 'IDebugObject:: IsNullReference |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::IsNullReference
helpviewer_keywords:
- IDebugObject::IsNullReference method
ms.assetid: 6dbfcdb0-954f-4486-8fac-7ea8d003e3a9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 844e6c92385c1aa719d3c9d0ff399db9104dccc0
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102161512"
---
# <a name="idebugobjectisnullreference"></a>IDebugObject::IsNullReference
このオブジェクトが null 参照であるかどうかをテストします。

## <a name="syntax"></a>構文

```cpp
HRESULT IsNullReference( 
   BOOL* pfIsNull
);
```

```csharp
int IsNullReference(
   out int pfIsNull
);
```

## <a name="parameters"></a>パラメーター
`pfIsNull`\
入出力`TRUE`このオブジェクトが null 参照の場合は0以外 () を返します。それ以外の場合は 0 () を返し `FALSE` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 Null 参照は、空のオブジェクト、またはに割り当てられていないオブジェクトを意味します。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
