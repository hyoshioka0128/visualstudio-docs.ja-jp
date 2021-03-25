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
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 63d75eae9c7966bfc5e7fceea0512db0fa174066
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105054102"
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

## <a name="remarks"></a>注釈
 配列内の値は、既存の値を置き換えて、この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトにコピーされます。 新しい値のサイズは、既存の値より大きくしたり小さくしたりすることができます。 `IDebugObject`Null 参照を指定することはできません。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
