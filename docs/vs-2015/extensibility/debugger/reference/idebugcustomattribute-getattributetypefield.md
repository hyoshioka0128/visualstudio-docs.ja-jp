---
title: 'IDebugCustomAttribute:: GetAttributeTypeField |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugCustomAttribute::GetAttributeTypeField
helpviewer_keywords:
- IDebugCustomAttribute::GetAttributeTypeField
ms.assetid: d6ce26d5-42ba-44c1-8659-0516db5bc82d
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: a56a148342eb659a4f57d68581159f64ee3b1226
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62568928"
---
# <a name="idebugcustomattributegetattributetypefield"></a>IDebugCustomAttribute::GetAttributeTypeField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

カスタム属性クラスの型を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetAttributeTypeField(   
   IDebugClassField** ppCAType  
);  
```  
  
```csharp  
int GetAttributeTypeField(  
   out IDebugClassField ppCAType  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppCAType`  
 入出力カスタム属性がインスタンスであるクラスを表す [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 カスタム属性は常にクラスです。 このメソッドは、そのクラスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトへのアクセスを提供します。  
  
## <a name="see-also"></a>参照  
 [IDebugCustomAttribute](../../../extensibility/debugger/reference/idebugcustomattribute.md)   
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)
