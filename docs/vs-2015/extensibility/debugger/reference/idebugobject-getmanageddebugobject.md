---
title: 'IDebugObject:: GetManagedDebugObject |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugObject::GetManagedDebugObject
helpviewer_keywords:
- IDebugObject::GetManagedDebugObject method
ms.assetid: cb89692e-7657-47ff-846d-311943521951
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 4f2917135f5e25648cf08cd9030e3fdf31aedb52
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68162472"
---
# <a name="idebugobjectgetmanageddebugobject"></a>IDebugObject::GetManagedDebugObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグエンジンのアドレス空間にマネージオブジェクトのコピーを作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetManagedDebugObject(   
   IDebugManagedObject** ppObject  
);  
```  
  
```csharp  
int GetManagedDebugObject(  
   out IDebugManagedObject ppObject  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppObject`  
 入出力新しく作成されたマネージオブジェクトを表す [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) がマネージ値クラスのインスタンスを表していない場合は E_FAIL を返します。  
  
## <a name="remarks"></a>注釈  
 この [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md) オブジェクトは、インスタンスなどのマネージ値クラスのインスタンスを表す必要があり `System.Decimal` ます。 ローカルコピーを用意することで、 [Evaluate](../../../extensibility/debugger/reference/idebugfunctionobject-evaluate.md) 呼び出しのオーバーヘッドが解消されます。  
  
## <a name="see-also"></a>参照  
 [IDebugObject](../../../extensibility/debugger/reference/idebugobject.md)   
 [IDebugManagedObject](../../../extensibility/debugger/reference/idebugmanagedobject.md)
