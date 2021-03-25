---
description: 配列内の要素の数を取得します。
title: 'IDebugArrayObject:: GetCount |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetCount
helpviewer_keywords:
- IDebugArrayObject::GetCount method
ms.assetid: 7931f3f7-033c-4bf8-8abd-95183952ebb0
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c3a5d052fcb2c40f9dad76791aa992dbfbde72b0
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058899"
---
# <a name="idebugarrayobjectgetcount"></a>IDebugArrayObject::GetCount
配列内の要素の数を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetCount( 
   DWORD* pdwElements
);
```

```csharp
int GetCount(
   out uint pdwElements
);
```

## <a name="parameters"></a>パラメーター
`pdwElements`\
入出力カウントを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドは、配列オブジェクトが多次元であっても、配列オブジェクトのすべての要素を1次元配列として表示します。 たとえば、配列の場合 `myarray[3][2][6]` 、このメソッドはパラメーターで36を返し `pdwElements` ます。 [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md)メソッドを使用して、一度に1つずつ個別の要素を取得します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
