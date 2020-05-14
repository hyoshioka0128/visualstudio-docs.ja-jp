---
title: Iデバッグメモリコンテキスト2::追加 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryContext2::Add
helpviewer_keywords:
- IDebugMemoryContext2::Add method
- Add method
ms.assetid: 3c47e646-ce9e-4dd3-8f1a-6dbd3827d407
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: a21fa2ec6d48bb1d6bf17bbc0d2ebf0d90a25a9f
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727486"
---
# <a name="idebugmemorycontext2add"></a>IDebugMemoryContext2::Add
指定した値を現在のコンテキストに追加し、新しいコンテキストを返します。

## <a name="syntax"></a>構文

```cpp
HRESULT Add( 
   UINT64                 dwCount,
   IDebugMemoryContext2** ppMemCxt
);
```

```csharp
int Add(
   ulong                    dwCount,
   out IDebugMemoryContext2 ppMemCxt
);
```

## <a name="parameters"></a>パラメーター
`dwCount`\
[in]現在のコンテキストに追加する値。

`ppMemCxt`\
[アウト]新しい[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)オブジェクトを返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 メモリ コンテキストはアドレスであるため、アドレスに値を追加すると、新しいコンテキスト インターフェイスを必要とする新しいアドレスが生成されます。

 このメソッドは、結果として得られるアドレスがこのコンテキストに関連付けられたメモリ空間の外にある場合でも、常に新しいコンテキストを生成する必要があります。 唯一の例外は、新しいコンテキストにメモリを割り当てることができない場合、`ppMemCxt`または null 値 (エラー) の場合です。

## <a name="see-also"></a>関連項目
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
