---
description: このメソッドは、このフィールドと指定したフィールドを比較し、等しいかどうかを比較します。
title: 'IDebugField:: Equal |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 58673703fa0e585095c9a82fe2c7a4bc3e14827c
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105077110"
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

## <a name="see-also"></a>こちらもご覧ください
- [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
