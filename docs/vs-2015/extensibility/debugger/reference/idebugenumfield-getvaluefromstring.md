---
title: 'IDebugEnumField:: GetValueFromString |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetValueFromString
helpviewer_keywords:
- IDebugEnumField::GetValueFromString method
ms.assetid: 1ef8ac5e-a3e0-4078-b876-7f5615aedcbb
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f553b7f019dd89af771e057a46a11b1affed1308
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188939"
---
# <a name="idebugenumfieldgetvaluefromstring"></a>IDebugEnumField::GetValueFromString
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、列挙定数の名前に関連付けられている値を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetValueFromString(  
   LPCOLESTR  pszValue,  
   ULONGLONG* pvalue  
);  
```  
  
```csharp  
int GetValueFromString(  
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
 このメソッドでは、大文字と小文字が区別されます。 大文字と小文字を区別しない検索が必要な場合 (たとえば、名前が大文字と小文字を区別しない Visual Basic などの言語) は、 [Getvaluefromstringcaseinsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)を使用します。  
  
## <a name="see-also"></a>参照  
 [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)   
 [GetValueFromStringCaseInsensitive](../../../extensibility/debugger/reference/idebugenumfield-getvaluefromstringcaseinsensitive.md)
