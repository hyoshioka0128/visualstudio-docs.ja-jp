---
title: フィールド::値から取得 |マイクロソフトドキュメント
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 5de59c573f7e233ea2aacb0dfa38826051c59373
ms.sourcegitcommit: 16a4a5da4a4fd795b46a0869ca2152f2d36e6db2
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 04/06/2020
ms.locfileid: "80730287"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
このメソッドは、列挙定数の値を指定して名前を取得します。

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
[in]列挙定数の名前を取得する値。

`pbstrValue`\
[アウト]列挙定数の名前を返します。

## <a name="return-value"></a>戻り値
 成功した場合は`S_OK`、 を返します。それ以外の`S_FALSE`場合は、値に関連付けられた名前がない場合に返すか、エラー コードを返します。

## <a name="remarks"></a>Remarks
 同じ値に複数の名前が関連付けられている場合は、列挙体に定義されている名が返されます。

## <a name="see-also"></a>関連項目
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
