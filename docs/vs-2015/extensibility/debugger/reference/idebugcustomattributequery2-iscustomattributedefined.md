---
title: 'IDebugCustomAttributeQuery2:: IsCustomAttributeDefined |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
helpviewer_keywords:
- IDebugCustomAttributeQuery2::IsCustomAttributeDefined
ms.assetid: 5c07cc52-6d2d-42df-9d76-9f1f769641db
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 6ef6a04d263e322d408bb7d7c95da1929d89010c
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62569320"
---
# <a name="idebugcustomattributequery2iscustomattributedefined"></a>IDebugCustomAttributeQuery2::IsCustomAttributeDefined
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

カスタム属性が名前によって存在するかどうかを判断します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT IsCustomAttributeDefined(   
   LPCOLESTR pszCustomAttributeName  
);  
```  
  
```csharp  
int IsCustomAttributeDefined(  
   [In] string pszCustomAttributeName  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pszCustomAttributeName`  
 から検索するカスタム属性の名前を格納している文字列。  
  
## <a name="return-value"></a>戻り値  
 このフィールドにカスタム属性が定義されている場合は S_OK を返し、それ以外の場合は S_FALSE を返します。  
  
## <a name="remarks"></a>注釈  
 カスタム属性に関連付けられている属性のバイト数を取得するには、 [GetCustomAttributeByName](../../../extensibility/debugger/reference/idebugcustomattributequery2-getcustomattributebyname.md) メソッドを呼び出します。  
  
## <a name="see-also"></a>参照  
 [IDebugCustomAttributeQuery2](../../../extensibility/debugger/reference/idebugcustomattributequery2.md)
