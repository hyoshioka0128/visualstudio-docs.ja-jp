---
title: 'IDebugClassField:: Enumの実装 |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugClassField::EnumInterfacesImplemented
helpviewer_keywords:
- IDebugClassField::EnumInterfacesImplemented method
ms.assetid: e5523e45-d350-491e-a92c-fe0ca97d2052
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 45cdc4ea3d1dad911179ce7b2a4926248ee921fd
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68191015"
---
# <a name="idebugclassfieldenuminterfacesimplemented"></a>IDebugClassField::EnumInterfacesImplemented
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このクラスによって実装されるインターフェイスの列挙子を作成します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT EnumInterfacesImplemented(   
   IEnumDebugFields** ppEnum  
);  
```  
  
```csharp  
int EnumInterfacesImplemented(  
   out IEnumDebugFields ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力実装されているインターフェイスの一覧を表す [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md) オブジェクトを返します。 インターフェイスが存在しない場合は、null 値を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合、は S_OK を返します。または、このクラスに実装されているインターフェイスがない場合は S_FALSE を返します。 それ以外の場合はエラー コードを返します。  
  
## <a name="remarks"></a>注釈  
 列挙体の各要素は、インターフェイスを記述する [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md) オブジェクトです。 アンマネージ [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] コードでは、インターフェイスを不連続エンティティとして使用しないので、このメソッドは常にアンマネージコードに対して null 値を返し [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] ます。  
  
## <a name="see-also"></a>参照  
 [IDebugClassField](../../../extensibility/debugger/reference/idebugclassfield.md)   
 [IEnumDebugFields](../../../extensibility/debugger/reference/ienumdebugfields.md)
