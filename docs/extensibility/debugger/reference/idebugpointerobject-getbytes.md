---
description: 連続する一連のバイトとしてポイントされている値を取得します。
title: 'IDebugPointerObject:: GetBytes |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugPointerObject::GetBytes
helpviewer_keywords:
- IDebugPointerObject::GetBytes method
ms.assetid: e986c188-87fb-4b51-86e9-ee6a0035bdab
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 51d5e4cf65c9e72dada225e042f7d3d11e9b4b4c
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102169679"
---
# <a name="idebugpointerobjectgetbytes"></a>IDebugPointerObject::GetBytes
連続する一連のバイトとしてポイントされている値を取得します。

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
からが指すオブジェクトの先頭からのオフセット (バイト単位)。

`dwCount`\
から取得するバイト数。

`pBytes`\
[入力、出力]値を連続した一連のバイトとして格納する配列。これは、指定されたオブジェクトからの指定されたオフセットから始まります。

`pdwBytes`\
入出力実際に取得されたバイト数を返します。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 このメソッドは、この [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md) によって表されるポインターがプリミティブ型またはプリミティブ型の単純な配列 (つまり、単純なバイトシーケンスで表すことができる配列) を指している場合に使用されます。

## <a name="see-also"></a>関連項目
- [IDebugPointerObject](../../../extensibility/debugger/reference/idebugpointerobject.md)
- [SetBytes](../../../extensibility/debugger/reference/idebugpointerobject-setbytes.md)
