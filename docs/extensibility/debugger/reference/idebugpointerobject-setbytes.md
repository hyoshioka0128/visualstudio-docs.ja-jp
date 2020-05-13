---
title: オブジェクトを設定します。マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::SetBytes
helpviewer_keywords:
- IDebugPointerObject::SetBytes method
ms.assetid: 8c578b38-38d7-46f3-bb2e-8a730fccd334
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: dede3ee5291afbfbeab4d6e60dcbd56e205e4526
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80725503"
---
# <a name="idebugpointerobjectsetbytes"></a>IDebugPointerObject::SetBytes
連続する一連のバイトから指す値を設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetBytes( 
   DWORD  dwStart,
   DWORD  dwCount,
   BYTE*  pBytes,
   DWORD* pdwBytes
);
```

```csharp
int SetBytes(
   uint     dwStart,
   uint     dwCount,
   byte[]   pBytes,
   out uint pdwBytes
);
```

## <a name="parameters"></a>パラメーター
`dwStart`\
[in]指すオブジェクトの先頭からのオフセット (バイト単位)。

`dwCount`\
[in]設定するバイト数。

`pBytes`\
[in]新しい値を表すバイト配列。 この値は、指定されたオフセットからオブジェクトに格納されます。

`pdwBytes`\
[アウト]実際に設定されたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 このメソッドは、この[IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)で表されるポインターが、プリミティブ型またはプリミティブ型の単純な配列 (つまり、バイトシーケンスで表すことができる配列) を指している場合に使用されます。 この`IDebugPointerObject`オブジェクトは null 参照にできません (メモリ内のアドレスを指している必要があります)。

## <a name="see-also"></a>関連項目
- [GetBytes](../../../extensibility/debugger/reference/idebugpointerobject-getbytes.md)
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
