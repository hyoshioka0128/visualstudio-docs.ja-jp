---
description: このメソッドは、値を指定して、列挙定数の名前を取得します。
title: 'IDebugEnumField:: GetStringFromValue |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: acangialosi
ms.author: anthc
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 8601be6a1c87fcad10c6e5260e791fcf2ce42f01
ms.sourcegitcommit: 4b323a8a8bfd1a1a9e84f4b4ca88fa8da690f656
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/05/2021
ms.locfileid: "102153340"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
このメソッドは、値を指定して、列挙定数の名前を取得します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetStringFromValue(
   ULONGLONG value,
   BSTR*     pbstrValue
);
```

```csharp
int GetStringFromValue(
   ulong      value,
   out string pbstrValue
);
```

## <a name="parameters"></a>パラメーター
`value`\
から列挙定数の名前を取得する対象の値。

`pbstrValue`\
入出力列挙定数の名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は、を返し `S_OK` ます。それ以外の場合は、 `S_FALSE` 値に関連付けられた名前がない場合はを返し、エラーコードを返します。

## <a name="remarks"></a>解説
 同じ値に複数の名前が関連付けられている場合は、列挙体で定義されている最初の名前が返されます。

## <a name="see-also"></a>関連項目
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
