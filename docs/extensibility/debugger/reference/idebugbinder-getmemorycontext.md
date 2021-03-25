---
description: このメソッドは、オブジェクトの場所またはメモリアドレスをメモリコンテキストに変換します。
title: 'IDebugBinder:: GetMemoryContext |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugBinder::GetMemoryContext
helpviewer_keywords:
- IDebugBinder::GetMemoryContext method
ms.assetid: 801c5b60-acff-4822-b23d-e9c7bbca8a0f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5a9fe7c0ee2d7902d24df1bdea773b4b2745a96f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067453"
---
# <a name="idebugbindergetmemorycontext"></a>IDebugBinder::GetMemoryContext
このメソッドは、オブジェクトの場所またはメモリアドレスをメモリコンテキストに変換します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetMemoryContext( 
   IDebugField*           pField,
   DWORD                  dwConstant,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int GetMemoryContext(
   IDebugField              pField,
   uint                     dwConstant,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>パラメーター
`pField`\
から検索するオブジェクトを記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 。 の場合は `NULL` 、代わりにを使用し `dwConstant` ます。

`dwConstant`\
から定数のメモリアドレス (0x5000 など)。

`ppMemCxt`\
入出力オブジェクトのアドレス、またはメモリ内のアドレスを表す [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) インターフェイスを返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugBinder](../../../extensibility/debugger/reference/idebugbinder.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
