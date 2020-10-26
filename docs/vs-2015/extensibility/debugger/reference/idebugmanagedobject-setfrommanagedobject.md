---
title: 'IDebugManagedObject:: SetFromManagedObject |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugManagedObject::SetFromManagedObject
helpviewer_keywords:
- IDebugManagedObject::SetFromManagedObject method
ms.assetid: 8700ee8d-2704-4580-bccc-046837a24edd
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 5fa81c34f18d6f1d3980da8d53c65f5ef58c05f3
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180594"
---
# <a name="idebugmanagedobjectsetfrommanagedobject"></a>IDebugManagedObject::SetFromManagedObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

パラメーターとして指定された値クラスのインスタンスから、値クラスオブジェクトのインスタンスの値を設定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT SetFromManagedObject(   
   IUnknown* pManagedObject  
);  
```  
  
```csharp  
int SetFromManagedObject(  
   object pManagedObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pManagedObject`  
 から新しい値を格納しているマネージオブジェクトを表すインターフェイス。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) オブジェクトによって表されるマネージオブジェクトを変更するために使用されます。  
  
## <a name="see-also"></a>参照  
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
