---
title: 'IPropertyProxyEESide:: Inplace Updateobject |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
helpviewer_keywords:
- IPropertyProxyEESide::InPlaceUpdateObject
ms.assetid: abf89411-1853-4f23-b244-d5e0afa197b1
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: c91497815dd18dc138b2eadc462c43785830a033
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199518"
---
# <a name="ipropertyproxyeesideinplaceupdateobject"></a>IPropertyProxyEESide::InPlaceUpdateObject
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

指定されたデータオブジェクトを使用してオブジェクトのデータを更新し、オブジェクトの新しいデータを表す新しいデータオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT InPlaceUpdateObject(  
   [in] IEEDataStorage*   dataIn,  
   [out] IEEDataStorage** dataOut  
);  
```  
  
```csharp  
int InPlaceUpdateObject(  
   IEEDataStorage     dataIn,  
   out IEEDataStorage dataOut  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dataIn`  
 から新しいデータを格納する [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクト。  
  
 `dataOut`  
 入出力 `IEEDataStorage` 置き換えられたデータを格納している新しいオブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、実際にオブジェクトのデータを更新します。 返された [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトのデータは、受信オブジェクトのデータと同じである必要はありません `IEEDataStorage` が、返されたオブジェクトにはプロパティの現在の値が反映されている必要があります。  
  
 受信データオブジェクトは、通常、EE によって実装されていません。 ただし、このメソッドによって返されるオブジェクトは常に EE によって実装されます。これにより、EE は `IEEDataStorage` 任意のクラスで必要なインターフェイスを実装できます。  
  
 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)メソッドは、受信データオブジェクトに基づいてデータオブジェクトを作成しますが、プロパティの元のデータには影響しません。  
  
## <a name="see-also"></a>参照  
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)   
 [CreateReplacementObject](../../../extensibility/debugger/reference/ipropertyproxyeeside-createreplacementobject.md)
