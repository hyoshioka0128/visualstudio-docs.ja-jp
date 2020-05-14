---
title: メモリバイト2::書き込み |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::WriteAt
helpviewer_keywords:
- IDebugMemoryBytes2::WriteAt method
- WriteAt method
ms.assetid: 61cc3704-47fa-4d9b-aa62-bb4585ac8fb1
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: ac9113424c6cd5cce230774a6e5335ffa4d4ba77
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80727521"
---
# <a name="idebugmemorybytes2writeat"></a>IDebugMemoryBytes2::WriteAt
指定したアドレスから始まる、指定したバイト数のメモリを書き込みます。

## <a name="syntax"></a>構文

```cpp
HRESULT WriteAt( 
   IDebugMemoryContext2* pStartContext,
   DWORD                 dwCount,
   BYTE*                 rgbMemory
);
```

```csharp
int WriteAt(
   IDebugMemoryContext2 pStartContext,
   uint                 dwCount,
   byte[]               rgbMemory
);
```

## <a name="parameters"></a>パラメーター
`pStartContext`\
[in]バイトの書き込みを開始する場所を指定する[IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)オブジェクト。

`dwCount`\
[in]書き込むバイト数。

`rgbMemory`\
[in]書き込むバイト。 この配列は、バイトサイズが少`dwCount`なくともバイトであると想定されます。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の`S_FALSE`場合は、すべてのバイトが書き込まれなかった場合に戻`E_FAIL`るか、エラー コード (通常は) を返します。

## <a name="remarks"></a>Remarks
 開始アドレスがこの[IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)オブジェクトで表されるメモリ ウィンドウ内にない場合は、書き込みが行われ`E_FAIL`ず、書き込み量がメモリ空間に重なっていても、 のエラー コードが返されます。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
- [IDebugMemoryContext2](../../../extensibility/debugger/reference/idebugmemorycontext2.md)
