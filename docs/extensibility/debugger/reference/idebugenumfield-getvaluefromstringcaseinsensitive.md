---
description: このメソッドは、大文字と小文字を区別しない検索を使用して、列挙定数の名前に関連付けられている値を返します。
title: 'IDebugEnumField:: GetValueFromStringCaseInsensitive |Microsoft Docs'
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
author: leslierichardson95
ms.author: lerich
manager: jmartens
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: 80ded5237cfc0fe1b03ae5175ca0c92a188538ab
ms.sourcegitcommit: f2916d8fd296b92cc402597d1d1eecda4f6cccbf
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 03/25/2021
ms.locfileid: "105065991"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
このメソッドは、大文字と小文字を区別しない検索を使用して、列挙定数の名前に関連付けられている値を返します。

## <a name="syntax"></a>構文

```cpp
HRESULT GetValueFromStringCaseInsensitive(
   LPCOLESTR  pszValue,
   ULONGLONG* pvalue
);
```

```csharp
int GetValueFromStringCaseInsensitive(
   string    pszValue,
   out ulong pValue
);
```

## <a name="parameters"></a>パラメーター
`pszValue`\
から値を取得する対象の名前を指定する文字列。 C++ では、これはワイド文字列です。

`pValue`\
入出力関連付けられている数値を返します。

## <a name="return-value"></a>戻り値
 成功した場合はを返し `S_OK` ます。それ以外の場合はを返します。 `S_FALSE` 名前が列挙に含まれていない場合は、またはエラーコードを返します。

## <a name="remarks"></a>注釈
 このメソッドでは、大文字と小文字は区別されません。 大文字と小文字を区別する検索が必要な場合 (たとえば、C++ などの言語で名前に大文字と小文字が区別される場合) は、 [Getvaluefromstring](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)を使用します。

## <a name="see-also"></a>こちらもご覧ください
- [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
- [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
