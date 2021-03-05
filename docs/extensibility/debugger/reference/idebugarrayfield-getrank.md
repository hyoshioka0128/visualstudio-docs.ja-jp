---
description: 配列の次元のランクまたは数を取得します。
title: 'IDebugArrayField:: Ge/k |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: d9e3d822bac6fa16314f5d2962d69adbf74d0bc3
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102143715"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
配列の次元のランクまたは数を取得します。

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
 配列のランクは、次元の数に対応します。 C++ および C# では、多次元配列は配列の配列であるため、1次元配列と見なされることがあり `GetRank` ます (メソッドは常に1を返します)。 一方、では、 [!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)] 多次元配列は異なる方法で処理され、そのような配列のランクは次元の数を反映し `GetRank` ます (メソッドは常に次元数を返します)。

## <a name="see-also"></a>関連項目
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
