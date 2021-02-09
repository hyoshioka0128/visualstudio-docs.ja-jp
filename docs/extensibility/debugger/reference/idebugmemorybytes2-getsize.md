---
title: 'IDebugMemoryBytes2:: GetSize |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugMemoryBytes2::GetSize
helpviewer_keywords:
- IDebugMemoryBytes2::GetSize method
- GetSize method
ms.assetid: dae64c5f-5b54-40c3-b32f-ec3b16c093f7
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 790fcccd54aa80c51137655b0653970897f496d9
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99909950"
---
# <a name="idebugmemorybytes2getsize"></a>IDebugMemoryBytes2::GetSize
この [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md) オブジェクトによって表されるメモリのサイズ (バイト単位) を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetSize( 
   UINT64* pqwSize
);
```

```csharp
int GetSize(
   out ulong pqwSize
);
```

## <a name="parameters"></a>パラメーター
`pqwSize`\
入出力メモリ領域のサイズ (バイト単位) を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugMemoryBytes2](../../../extensibility/debugger/reference/idebugmemorybytes2.md)
