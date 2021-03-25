---
description: 配列内の次元数を指定して、各インデックスのベースインデックス (下限) を取得します。
title: 'IDebugArrayObject2:: GetBaseIndices |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
helpviewer_keywords:
- GetBaseIndices
- IDebugArrayObject2::GetBaseIndices
ms.assetid: 882951a2-3da0-49bf-8d1e-7daedd13ffe6
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 3843b93bb9255c28b8ca083af37a3ba4ecbd7f7e
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105067557"
---
# <a name="idebugarrayobject2getbaseindices"></a>IDebugArrayObject2::GetBaseIndices
配列内の次元数を指定して、各インデックスのベースインデックス (下限) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBaseIndices (
   DWORD  dwRank,
   DWORD* dwIndices
);
```

```csharp
int GetBaseIndices (
   uint       dwRank,
   out uint[] dwIndices
);
```

## <a name="parameters"></a>パラメーター
`dwRank`\
から配列の次元数 (ランク)。

`dwIndices`\
入出力配列のベースインデックス (下限)。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="remarks"></a>注釈
 例として、この関数は、次の C# コードによって作成された配列に対して ' 5 ' を返します。

```
int[] lengths = { 12 };
int[] lowerbounds = { 5 };
Array.CreateInstance(typeof(int), lengths, lowerbounds);
```

## <a name="see-also"></a>こちらもご覧ください
- [IDebugArrayObject2](../../../extensibility/debugger/reference/idebugarrayobject2.md)
