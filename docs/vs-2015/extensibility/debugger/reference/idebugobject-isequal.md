---
title: 'IDebugObject:: IsEqual |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::IsEqual
helpviewer_keywords:
- IDebugObject::IsEqual method
ms.assetid: 4b76e663-ef2e-41ff-9be1-bf26d666a34a
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 85252cdaf9fb076ebd4f8000115bcea576531bb1
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68159119"
---
# <a name="idebugobjectisequal"></a>IDebugObject::IsEqual
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

オブジェクトとこのオブジェクトを比較します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT IsEqual(   
   IDebugObject* pObject,  
   BOOL*         pfIsEqual  
);  
```  
  
```csharp  
int IsEqual(  
   IDebugObject pObject,  
   out int      pfIsEqual  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pObject`  
 からと比較するオブジェクトを表す [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクト。  
  
 `pfIsEqual`  
 入出力`TRUE`オブジェクトの値が等しい場合は0以外 () を返します。それ以外の場合は 0 () を返し `FALSE` ます。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 通常、このメソッドは、パラメーターとこの IDebugObject オブジェクトによって表される値のアドレスを比較できます `pObject` 。アドレスが等しい場合は、それらのオブジェクトが等しいと見なされます。 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)  
  
## <a name="see-also"></a>参照  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)
