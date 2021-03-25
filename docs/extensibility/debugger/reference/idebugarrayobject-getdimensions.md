---
description: 配列の次元を取得します。
title: 'IDebugArrayObject:: GetDimensions |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetDimensions
helpviewer_keywords:
- IDebugArrayObject::GetDimensions method
ms.assetid: 113e0aff-9028-49d6-b104-9fe7be4772d7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: 7ba82b8a921a7295b6521622ff45efc84a9b6742
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105058886"
---
# <a name="idebugarrayobjectgetdimensions"></a>IDebugArrayObject::GetDimensions
配列の次元を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetDimensions( 
   DWORD dwCount,
   DWORD dwDimensions[]
);
```

```csharp
int GetDimensions(
   [In] uint    dwCount,
   [Out] uint[] dwDimensions
);
```

## <a name="parameters"></a>パラメーター
`dwCount`\
から取得する次元の数。

`dwDimensions`\
[入力、出力]各次元のサイズを格納する配列。 `dwCount` 配列の最大サイズを指定し `dwDimensions` ます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>注釈
 多次元配列のサイズは、次元ごとに異なる場合があります。 たとえば、3次元配列の場合、 `myarray[3][2][6]` このメソッドは、パラメーターの3、2、および6をこの `dwDimensions` 順序で返します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
