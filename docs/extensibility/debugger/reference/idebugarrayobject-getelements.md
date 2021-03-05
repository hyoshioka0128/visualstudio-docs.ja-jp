---
description: 配列のすべての要素の列挙子を取得します。
title: 'IDebugArrayObject:: GetElements |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 33840f3f5d5a65cf1ed929049f0b85801724a5c9
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158554"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
配列のすべての要素の列挙子を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetElements( 
   IEnumDebugObjects** ppEnum
);
```

```csharp
int GetElements(
   out IEnumDebugObjects ppEnum
);
```

## <a name="parameters"></a>パラメーター
`ppEnum`\
入出力すべての要素を列挙できる [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 別の方法として、 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) メソッドと [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) メソッドを使用して、要素を反復処理します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
