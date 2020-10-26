---
title: 'IDebugManagedObject:: GetManagedObject |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugManagedObject::GetManagedObject
helpviewer_keywords:
- IDebugManagedObject::GetManagedObject method
ms.assetid: 6abe1402-6aad-41e6-8ec1-ae12d5945992
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 74390d4c5f27400b0549408b1c36e9e385b3e60b
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68180607"
---
# <a name="idebugmanagedobjectgetmanagedobject"></a>IDebugManagedObject::GetManagedObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

マネージオブジェクトを表すインターフェイスを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetManagedObject(   
   IUnknown** ppManagedObject  
);  
```  
  
```cpp#  
int GetManagedObject(  
   out object ppManagedObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppManagedObject`  
 入出力マネージオブジェクトを表すインターフェイスを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドから返されるインターフェイスは、マネージクラスによって実装されたインターフェイスに対してクエリを実行できるため、そのメソッドを呼び出すことができます。  
  
## <a name="see-also"></a>参照  
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
