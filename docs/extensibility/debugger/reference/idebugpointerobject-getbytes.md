---
title: オブジェクトを取得します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 17bc39f65d7c4c42b4f958b559df7c5b7d3bbdf7
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725518"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
連続する一連のバイトとして指す値を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int GetBytes(
   uint       dwStart,
   uint       dwCount,
   out byte[] pBytes,
   out uint   pdwBytes
);
```

## <a name="parameters"></a>パラメーター
`dwStart`\
[in]指すオブジェクトの先頭からのオフセット (バイト単位)。

`dwCount`\
[in]取得するバイト数。

`pBytes`\
[イン、アウト]値を連続したバイトとして格納する配列。

`pdwBytes`\
[アウト]実際に取得されたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、この[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)で表されるポインターが、プリミティブ型またはプリミティブ型の単純な配列 (つまり、バイトシーケンスで表すことができる配列) を指している場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [バイト数を設定](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
