---
title: 'IPropertyProxyEESide:: InitSourceDataProvider |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
helpviewer_keywords:
- IPropertyProxyEESide::InitSourceDataProvider
ms.assetid: 5156f593-5052-4e3a-9d02-081916fb342d
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: f5e067a0b93656eecd1fe47d5b192c70916b672d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68199507"
---
# <a name="ipropertyproxyeesideinitsourcedataprovider"></a>IPropertyProxyEESide::InitSourceDataProvider
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このオブジェクトのソースデータを初期化し、初期データを格納しているオブジェクトを返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT InitSourceDataProvider(  
   IEEDataStorage** dataOut  
);  
```  
  
```csharp  
int InitSourceDataProvider(  
   out IEEDataStorage dataOut  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `dataOut`  
 入出力 [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 このメソッドは、オブジェクトのデータに対して [Ieedatastorage](../../../extensibility/debugger/reference/ieedatastorage.md) インターフェイスを返すことができるように、オブジェクトを初期化するために必要なものをすべて実行します。 これにより、オブジェクトのデータを表示したり、許可されている場合は型ビジュアライザーによって変更したりできます。  
  
## <a name="see-also"></a>参照  
 [IPropertyProxyEESide](../../../extensibility/debugger/reference/ipropertyproxyeeside.md)   
 [IEEDataStorage](../../../extensibility/debugger/reference/ieedatastorage.md)
