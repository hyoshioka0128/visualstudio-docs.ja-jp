---
description: このメソッドは、このポインターオブジェクトが指すオブジェクトの型を返します。
title: 'IDebugPointerField:: GetDereferencedField |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: e54b378475cec191ca8395a7af5652ea6e93125f
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105053673"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
このメソッドは、このポインターオブジェクトが指すオブジェクトの型を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDereferencedField(
   IDebugField** ppField
);
```

```csharp
int GetDereferencedField(
   out IDebugField ppField
);
```

## <a name="parameters"></a>パラメーター
`ppField`\
入出力対象オブジェクトの型を記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 たとえば、 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) オブジェクトが整数を指している場合、このメソッドによって返される [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 型によってその整数型が記述されます。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
