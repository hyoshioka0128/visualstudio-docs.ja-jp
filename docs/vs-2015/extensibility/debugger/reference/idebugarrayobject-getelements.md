---
title: 'IDebugArrayObject:: GetElements |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetElements
helpviewer_keywords:
- IDebugArrayObject::GetElements method
ms.assetid: f6a6262f-5183-46ce-8a45-33ef46088b98
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: cad81d76e2fcec01fa50a37fa6ab6cb49cfc79be
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423700"
---
# <a name="idebugarrayobjectgetelements"></a>IDebugArrayObject::GetElements
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

配列のすべての要素の列挙子を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetElements(   
   IEnumDebugObjects** ppEnum  
);  
```  
  
```csharp  
int GetElements(  
   out IEnumDebugObjects ppEnum  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppEnum`  
 入出力すべての要素を列挙できる [IEnumDebugObjects](../../../extensibility/debugger/reference/ienumdebugobjects.md) オブジェクトを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 別の方法として、 [GetCount](../../../extensibility/debugger/reference/idebugarrayobject-getcount.md) メソッドと [GetElement](../../../extensibility/debugger/reference/idebugarrayobject-getelement.md) メソッドを使用して、要素を反復処理します。  
  
## <a name="see-also"></a>参照  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
