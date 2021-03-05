---
description: 指定された位置から始まるバイトシーケンスを読み取ります。
title: 'IDebugMemoryBytes2:: ReadAt |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::ReadAt
helpviewer_keywords:
- IDebugMemoryBytes2::ReadAt method
- ReadAt method
ms.assetid: b413684d-4155-4bd4-ae30-ffa512243b5f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f408e062fad4485fb159225e0639618d303e0806
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102165164"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
指定された位置から始まるバイトシーケンスを読み取ります。

## <a name="syntax"></a>構文

```cpp
HRESULT ReadAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory,
   DWORD*                pdwRead,
   DWORD*                pdwUnreadable
);
```

```csharp
int ReadAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory,
   out uint             pdwRead,
   ref uint             pdwUnreadable
);
```

## <a name="parameters"></a>パラメーター
`pStartContext`\
からバイトの読み取りを開始する位置を指定する [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクト。

`dwCount`\
から読み取るバイト数。 配列の長さも指定し `rgbMemory` ます。

`rgbMemory`\
[入力、出力]実際に読み取られたバイトを格納した配列。

`pdwRead`\
入出力実際に読み取られた連続するバイト数を返します。

`pdwUnreadable`\
[入力、出力]読み取り不可能なバイト数を返します。 クライアントが読み取り不可能なバイト数で興味場合、null 値を指定できます。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 100バイトが要求され、最初の50が読み取り可能である場合、次の20は読み取り不可能で、残りの30は読み取り可能であり、このメソッドはを返します。

 *`pdwRead` = 50

 *`pdwUnreadable` = 20

 この場合、呼び出し元 `*pdwRead + *pdwUnreadable < dwCount` は、要求された元の100の残りの30バイトを読み取るために追加の呼び出しを行う必要があります。また、パラメーターで渡される [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md) オブジェクトは、 `pStartContext` 70 によって高度である必要があります。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
