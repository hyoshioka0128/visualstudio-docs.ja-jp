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
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
ms.openlocfilehash: f5bb935ea4aba6ab6ebd0a39f8dfc8d539d6555c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158684"
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

## <a name="remarks"></a>解説
 多次元配列のサイズは、次元ごとに異なる場合があります。 たとえば、3次元配列の場合、 `myarray[3][2][6]` このメソッドは、パラメーターの3、2、および6をこの `dwDimensions` 順序で返します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
