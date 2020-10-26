---
title: 'IDebugEnumField:: GetStringFromValue |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugEnumField::GetStringFromValue
helpviewer_keywords:
- IDebugEnumField::GetStringFromValue method
ms.assetid: 5f95fd0c-fdce-497f-9f54-2ad8749494e9
caps.latest.revision: 6
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: ecdd60c363e30afbe4c61e8e18660a17a06a5ce8
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188991"
---
# <a name="idebugenumfieldgetstringfromvalue"></a>IDebugEnumField::GetStringFromValue
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、値を指定して、列挙定数の名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
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
  
#### <a name="parameters"></a>パラメーター  
 `value`  
 から列挙定数の名前を取得する対象の値。  
  
 `pbstrValue`  
 入出力列挙定数の名前を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は、を返し `S_OK` ます。それ以外の場合は、 `S_FALSE` 値に関連付けられた名前がない場合はを返し、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 同じ値に複数の名前が関連付けられている場合は、列挙体で定義されている最初の名前が返されます。  
  
## <a name="see-also"></a>参照  
 [IDebugEnumField](../../../extensibility/debugger/reference/idebugenumfield.md)
