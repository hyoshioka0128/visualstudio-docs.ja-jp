---
title: 'IDebugField:: Equal |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: c19e8860fb9ed9cbd65efe7fa72fd920a01622ff
ms.sourcegitcommit: ae6d47b09a439cd0e13180f5e89510e3e347fd47
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 02/08/2021
ms.locfileid: "99915482"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
このメソッドは、このフィールドと指定したフィールドを比較し、等しいかどうかを比較します。

## <a name="syntax"></a>構文

```cpp
HRESULT Equal( 
   IDebugField* pField
);
```

```csharp
int Equal(
   IDebugField pField
);
```

## <a name="parameters"></a>パラメーター
`pField`\
からこのと比較するフィールド。

## <a name="return-value"></a>戻り値
 フィールドが同じである場合、はを返し `S_OK` ます。 フィールドが異なる場合は、それ以外の場合は `S_FALSE.` エラーコードを返します。

## <a name="see-also"></a>関連項目
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
