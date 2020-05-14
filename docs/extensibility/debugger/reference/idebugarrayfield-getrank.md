---
title: を指定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugArrayField::GetRank
helpviewer_keywords:
- IDebugArrayField::GetRank method
ms.assetid: 2364b876-5be1-4bab-9b8f-3b6121da35c6
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 692f2f13d861d9688ba349fbc80cb1ca426582c1
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80736313"
---
# <a name="idebugarrayfieldgetrank"></a>IDebugArrayField::GetRank
配列のランクまたは次元数を取得します。

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
[アウト]ランクを返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 配列のランクは次元数に対応します。 C++ および C# では、多次元配列は実際には配列の配列であるため、1 次元配列と見なすことができます (メソッドは`GetRank`常に 1 を返します)。 一[!INCLUDE[vbprvb](../../../code-quality/includes/vbprvb_md.md)]方、多次元配列は異なる方法で処理され、そのような配列のランクは次元の数を反映します(`GetRank`そして、メソッドは常に次元の数を返します)。

## <a name="see-also"></a>関連項目
- [IDebugArrayField](../../../extensibility/debugger/reference/idebugarrayfield.md)
