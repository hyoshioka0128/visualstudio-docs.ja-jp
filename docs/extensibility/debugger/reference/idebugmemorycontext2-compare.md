---
title: Iデバッグメモリコンテキスト2::比較 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Compare
helpviewer_keywords:
- IDebugMemoryContext2::Compare method
- Compare method
ms.assetid: c51b5128-848e-4d8e-b2e9-1161339763c3
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 4b2551f8554d96186b90a1eed97a5a48ec5f0405
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727494"
---
# <a name="idebugmemorycontext2compare"></a>IDebugMemoryContext2::Compare
比較フラグで示される方法で、指定された配列の各コンテキストとメモリ コンテキストを比較し、最初に一致するコンテキストのインデックスを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Compare( 
   CONTEXT_COMPARE        compare,
   IDebugMemoryContext2** rgpMemoryContextSet,
   DWORD                  dwMemoryContextSetLen,
   DWORD*                 pdwMemoryContext
);
```

```csharp
int Compare(
   enum_CONTEXT_COMPARE   compare,
   IDebugMemoryContext2[] rgpMemoryContextSet,
   uint                   dwMemoryContextSetLen,
   out uint               pdwMemoryContext
);
```

## <a name="parameters"></a>パラメーター
`compare`\
[in]比較の種類を決定する[CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)列挙体の値。

`rgpMemoryContextSet`\
[in]比較対象の[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)オブジェクトへの参照の配列。

`dwMemoryContextSetLen`\
[in]配列内のコンテキストの`rgpMemoryContextSet`数。

`pdwMemoryContext`\
[アウト]比較を満たす最初のメモリ コンテキストのインデックスを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。 2`E_COMPARE_CANNOT_COMPARE`つのコンテキストを比較できない場合に返します。

## <a name="remarks"></a>Remarks
 デバッグ エンジン (DE) は、すべての種類の比較をサポートする必要はありませんが、少`CONTEXT_EQUAL`なくとも 、 `CONTEXT_LESS_THAN` `CONTEXT_GREATER_THAN` 、、および`CONTEXT_SAME_SCOPE`をサポートする必要があります。

## <a name="see-also"></a>関連項目
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
- [CONTEXT_COMPARE](../../../extensibility/debugger/reference/context-compare.md)
