---
description: このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。
title: 'IDebugObject2:: GetAlias |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject2::GetAlias
helpviewer_keywords:
- IDebugObject2::GetAlias method
ms.assetid: aa6824d5-c932-42ba-8713-950e7d1fb42f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8c2ac683a5fb4d694b7cf3ab84849b9d7c7df7a3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143130"
---
# <a name="idebugobject2getalias"></a>IDebugObject2::GetAlias
このオブジェクトに関連付けられているエイリアス (存在する場合) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetAlias(
   IDebugAlias** ppAlias
);
```

```csharp
int GetAlias(
   out IDebugAlias ppAlias
);
```

## <a name="parameters"></a>パラメーター
`ppAlias`\
入出力このオブジェクトの別名を表す [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md) オブジェクトを返します。それ以外の場合、は null 値を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 オブジェクトのエイリアスは、 [Createalias](../../../extensibility/debugger/reference/idebugobject2-createalias.md) メソッドの呼び出しを使用して作成されます。

## <a name="see-also"></a>関連項目
- [IDebugObject2](../../../extensibility/debugger/reference/idebugobject2.md)
- [IDebugAlias](../../../extensibility/debugger/reference/idebugalias.md)
