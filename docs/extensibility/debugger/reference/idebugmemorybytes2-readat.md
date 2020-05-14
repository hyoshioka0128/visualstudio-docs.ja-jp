---
title: メモリバイト2::リードアット |マイクロソフトドキュメント
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
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: f909ac3d2e2993879e4c24140abbf23c2ee8d545
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727534"
---
# <a name="idebugmemorybytes2readat"></a>IDebugMemoryBytes2::ReadAt
指定された位置から開始して、バイトシーケンスを読み取ります。

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
[in]バイトの読み取りを開始する場所を指定する[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)オブジェクト。

`dwCount`\
[in]読み取るバイト数。 また、配列の長さを`rgbMemory`指定します。

`rgbMemory`\
[イン、アウト]実際に読み取られたバイト数で配列が埋め込まれます。

`pdwRead`\
[アウト]実際に読み取られた連続したバイト数を返します。

`pdwUnreadable`\
[イン、アウト]読み取り不可能なバイト数を返します。 クライアントが読み取り不能バイト数に関心がない場合は、null 値になることがあります。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 100 バイトが要求され、最初の 50 が読み取り可能で、次の 20 バイトが読み取り不可能で、残りの 30 バイトが読み取り可能な場合、このメソッドは次の値を返します。

 *`pdwRead`= 50

 *`pdwUnreadable`= 20

 この場合、`*pdwRead + *pdwUnreadable < dwCount`呼び出し元は、要求された元の 100 の残りの 30 バイトを読み取るために追加の呼び出し`pStartContext`を行う必要があり、パラメーターに渡された[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)オブジェクトは 70 進める必要があります。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
