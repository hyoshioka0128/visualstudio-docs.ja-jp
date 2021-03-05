---
description: オブジェクトの値を連続する一連のバイトとして取得します。
title: 'IDebugObject:: GetValue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::GetValue
helpviewer_keywords:
- IDebugObject::GetValue method
ms.assetid: eec6051e-8ecb-49fa-bdd4-dd786f211692
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63e07ccfbcf2117363ed3e2096d5f0bb4bcac806
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102150446"
---
# <a name="idebugobjectgetvalue"></a>IDebugObject::GetValue
オブジェクトの値を連続する一連のバイトとして取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int GetValue(
   ref byte[] pValue,
   uint nSize
);
```

## <a name="parameters"></a>パラメーター
`pValue`\
[入力、出力]オブジェクトの値を表す連続する一連のバイトを格納する配列。

`nSize`\
からフェッチする最大バイト数。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 [GetSize](../../../extensibility/debugger/reference/idebugobject-getsize.md)メソッドを呼び出すことによってフェッチできる値の合計バイト数を取得します。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
