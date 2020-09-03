---
title: 'IDebugEnumField:: GetValueFromStringCaseInsensitive |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive
helpviewer_keywords:
- IDebugEnumField::GetValueFromStringCaseInsensitive method
ms.assetid: ef95b38e-d9b2-4fb5-a166-7c2e14641dc7
caps.latest.revision: 9
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: efe94a721c432cb1284df299ca267271ab5bef4d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188932"
---
# <a name="idebugenumfieldgetvaluefromstringcaseinsensitive"></a>IDebugEnumField::GetValueFromStringCaseInsensitive
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、大文字と小文字を区別しない検索を使用して、列挙定数の名前に関連付けられている値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 `pszValue`  
 から値を取得する対象の名前を指定する文字列。 C++ では、これはワイド文字列です。  
  
 `pValue`  
 入出力関連付けられている数値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はを返します。 `S_FALSE` 名前が列挙に含まれていない場合は、またはエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドでは、大文字と小文字は区別されません。 大文字と小文字を区別する検索が必要な場合 (たとえば、C++ などの言語で名前に大文字と小文字が区別される場合) は、 [Getvaluefromstring](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)を使用します。  
  
## <a name="see-also"></a>参照  
 [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)   
 [GetValueFromString](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstring.md)
