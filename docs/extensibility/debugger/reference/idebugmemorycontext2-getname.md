---
description: このコンテキストのユーザーが指定可能な名前を取得します。
title: 'IDebugMemoryContext2:: GetName |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::GetName
helpviewer_keywords:
- IDebugMemoryContext2::GetName method
- GetName method
ms.assetid: 8c212556-7d9e-4d68-b2a9-8212f50d0287
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 89d5d3cb1d2bed36a9e15f99644a02bdc308e0ee
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058613"
---
# <a name="idebugmemorycontext2getname"></a>IDebugMemoryContext2::GetName
このコンテキストのユーザーが指定可能な名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetName( 
   BSTR* pbstrName
);
```

```csharp
int GetName(
   out string pbstrName
);
```

## <a name="parameters"></a>パラメーター
`pbstrName`\
入出力メモリコンテキストの名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 通常、メモリコンテキストの名前は使用されません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
