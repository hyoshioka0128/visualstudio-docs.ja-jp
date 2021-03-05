---
description: 配列のランク (次元数) を取得します。
title: 'IDebugArrayObject:: Ge/k |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetRank
helpviewer_keywords:
- IDebugArrayObject::GetRank method
ms.assetid: 9948551a-e334-4ff6-979c-08dab633b9b6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3a246cda3f5b9395ae013b4bca9d4d27d6f8a5c1
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102158541"
---
# <a name="idebugarrayobjectgetrank"></a>IDebugArrayObject::GetRank
配列のランク (次元数) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetRank( 
   DWORD* pdwRank
);
```

```csharp
int GetRank(
   out uint pdwRank
);
```

## <a name="parameters"></a>パラメーター
`pdwRank`\
入出力ランクを返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [Getdimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)メソッドを使用して、配列オブジェクトの各次元のサイズを取得します。

## <a name="see-also"></a>関連項目
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
