---
title: 'IEnumDebugCodeContexts2:: Next |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IEnumDebugCodeContexts2::Next
helpviewer_keywords:
- IEnumDebugCodeContexts2::Next
ms.assetid: 0d8aa2db-0994-4166-b364-2e25d936fffc
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 1391ab12d3f362a3e3c7e6841fe627f403f0e38b
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99929486"
---
# <a name="ienumdebugcodecontexts2next"></a>IEnumDebugCodeContexts2::Next
列挙体から次の要素のセットを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Next(
   ULONG                celt,
   IDebugCodeContext2** rgelt,
   ULONG*               pceltFetched
);
```

```csharp
int Next(
   uint                 celt,
   IDebugCodeContext2[] rgelt,
   ref uint             pceltFetched
);
```

## <a name="parameters"></a>パラメーター
`celt`\
から取得する要素の数。 配列の最大サイズも指定し `rgelt` ます。

`rgelt`\
[入力、出力]入力する [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md) 要素の配列。

`pceltFetched`\
入出力で実際に返された要素の数を返し `rgelt` ます。

## <a name="return-value"></a>戻り値
 正常に終了した場合は、`S_OK` を返します。 要求された `S_FALSE` 数の要素を返すことができなかった場合は、を返します。それ以外の場合は、エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IEnumDebugCodeContexts2](../../../extensibility/debugger/reference/ienumdebugcodecontexts2.md)
- [IDebugCodeContext2](../../../extensibility/debugger/reference/idebugcodecontext2.md)
