---
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
ms.openlocfilehash: 10f42ca10496d89955032bd531651186d0aecf37
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99926354"
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
