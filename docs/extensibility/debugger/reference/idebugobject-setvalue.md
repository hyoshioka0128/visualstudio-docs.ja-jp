---
title: オブジェクト::セットバリュー |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugObject::SetValue
helpviewer_keywords:
- IDebugObject::SetValue method
ms.assetid: d652e09c-cdc1-4519-8116-d7c743f5679b
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 9e4652eb3c77a1871063dfa71b464fb1f7c43f94
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80726356"
---
# <a name="idebugobjectsetvalue"></a>IDebugObject::SetValue
連続するバイトからオブジェクトの値を設定します。

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
[in]新しい値を表すバイト配列。

`nSize`\
[in]値のサイズ (バイト単位)。

## <a name="return-value"></a>戻り値
 成功した場合は、S_OK返します。それ以外の場合は、エラー コードを返します。

## <a name="remarks"></a>Remarks
 配列内の値は、この[IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)オブジェクトにコピーされ、既存の値を置き換えます。 新しい値のサイズは、既存の値よりも大きく、または小さくすることができます。 NULL`IDebugObject`参照はできません。

## <a name="see-also"></a>関連項目
- [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
- [GetValue](../../../extensibility/debugger/reference/idebugobject-getvalue.md)
