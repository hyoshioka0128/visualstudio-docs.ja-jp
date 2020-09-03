---
title: 'IDebugGenericParamField:: GetNameOfFormalParam |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- IDebugGenericParamField::GetNameOfFormalParam
- GetNameOfFormalParam
ms.assetid: 05032a83-49ce-4007-b5d6-7b56945b956c
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: eb18022aa72b0384ce55c6febb0bca2d193c890a
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180686"
---
# <a name="idebuggenericparamfieldgetnameofformalparam"></a>IDebugGenericParamField::GetNameOfFormalParam
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このジェネリックパラメーターの名前を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetNameOfFormalParam (  
   BSTR* pbstrName  
);  
```  
  
```csharp  
int GetNameOfFormalParam (  
   string pbstrName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pbstrName`  
 入出力このジェネリックパラメーターの名前。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="example"></a>例  
 次の例は、 [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)インターフェイスを公開する**CDebugGenericParamFieldType**オブジェクトに対してこのメソッドを実装する方法を示しています。  
  
```cpp#  
HRESULT CDebugGenericParamFieldType::GetNameOfFormalParam(BSTR *pbstrName)  
{  
    HRESULT hr = S_OK;  
    CComBSTR bstrName;  
  
    METHOD_ENTRY( CDebugGenericParamFieldType::GetNameOfFormalParam );  
  
    IfFalseGo( pbstrName, E_INVALIDARG );  
    IfFailGo( this->LoadProps() );  
    IfNullGo( *pbstrName = SysAllocString(m_bstrName), E_OUTOFMEMORY );  
  
Error:  
  
    METHOD_EXIT( CDebugGenericParamFieldType::GetNameOfFormalParam, hr );  
    return hr;  
}  
```  
  
## <a name="see-also"></a>参照  
 [IDebugGenericParamField](../../../extensibility/debugger/reference/idebuggenericparamfield.md)
