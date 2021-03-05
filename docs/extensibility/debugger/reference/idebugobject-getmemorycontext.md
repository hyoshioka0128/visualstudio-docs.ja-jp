---
description: オブジェクトの値のアドレスを表すメモリコンテキストを取得します。
title: 'IDebugObject:: GetMemoryContext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetMemoryContext
helpviewer_keywords:
- IDebugObject::GetMemoryContext method
ms.assetid: 6760a0d3-a898-4e81-b68f-c45c584b225b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9fabcee7bc0f4501f1440345b648fb93dab84d16
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102172113"
---
# <a name="idebugobjectgetmemorycontext"></a>IDebugObject::GetMemoryContext
オブジェクトの値のアドレスを表すメモリコンテキストを取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMemoryContext( 
   IDebugMemoryContext2** pContext
);
```

```csharp
int GetMemoryContext(
   ref IDebugMemoryContext2 pContext
);
```

## <a name="parameters"></a>パラメーター
`pContext`\
入出力オブジェクトの値のアドレスを表す [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 返されるメモリコンテキストは、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトによって表される値のアドレスを指定します。

## <a name="see-also"></a>関連項目
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
