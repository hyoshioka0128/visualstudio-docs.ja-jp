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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1440ff2fa82c8296bf54b106b622556a8eebb611
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105094329"
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

## <a name="remarks"></a>注釈
 [Getdimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)メソッドを使用して、配列オブジェクトの各次元のサイズを取得します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
