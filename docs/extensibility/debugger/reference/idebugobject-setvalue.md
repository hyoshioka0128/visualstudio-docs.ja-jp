---
description: オブジェクトの値を連続する一連のバイトから設定します。
title: 'IDebugObject:: SetValue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 972281335b964679f38693182e42c4e64074dffa
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102167153"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
オブジェクトの値を連続する一連のバイトから設定します。

## <a name="syntax"></a>構文

```cpp
HRESULT SetValue( 
   BYTE* pValue,
   UINT  nSize
);
```

```csharp
int SetValue(
   byte[] pValue,
   uint   nSize
);
```

## <a name="parameters"></a>パラメーター
`pValue`\
から新しい値を表すバイト配列。

`nSize`\
から値のサイズ (バイト単位)。

## <a name="return-value"></a>戻り値
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。

## <a name="remarks"></a>解説
 配列内の値は、既存の値を置き換えて、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトにコピーされます。 新しい値のサイズは、既存の値より大きくしたり小さくしたりすることができます。 `IDebugObject`Null 参照を指定することはできません。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
