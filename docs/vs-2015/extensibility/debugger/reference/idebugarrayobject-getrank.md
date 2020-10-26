---
title: 'IDebugArrayObject:: Ge/k |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugArrayObject::GetRank
helpviewer_keywords:
- IDebugArrayObject::GetRank method
ms.assetid: 9948551a-e334-4ff6-979c-08dab633b9b6
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: bf9700e2c3b29561229999506ed789a2e3d6e52e
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62423674"
---
# <a name="idebugarrayobjectgetrank"></a>IDebugArrayObject::GetRank
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

配列のランク (次元数) を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetRank(   
   DWORD* pdwRank  
);  
```  
  
```csharp  
int GetRank(  
   out uint pdwRank  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwRank`  
 入出力ランクを返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合は S_OK を返します。それ以外の場合は、エラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 [Getdimensions](../../../extensibility/debugger/reference/idebugarrayobject-getdimensions.md)メソッドを使用して、配列オブジェクトの各次元のサイズを取得します。  
  
## <a name="see-also"></a>参照  
 [IDebugArrayObject](../../../extensibility/debugger/reference/idebugarrayobject.md)
