---
title: 'IDebugPointerField:: GetDereferencedField |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugPointerField::GetDereferencedField
helpviewer_keywords:
- IDebugPointerField::GetDereferencedField method
ms.assetid: 8de988ab-cd79-4287-be72-3c900f2fe407
caps.latest.revision: 8
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 02197f660189d4caf374fc5927f349fd5fc6b8b5
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68201014"
---
# <a name="idebugpointerfieldgetdereferencedfield"></a>IDebugPointerField::GetDereferencedField
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、このポインターオブジェクトが指すオブジェクトの型を返します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetDereferencedField(  
   IDebugField** ppField  
);  
```  
  
```csharp  
int GetDereferencedField(  
   out IDebugField ppField  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `ppField`  
 入出力対象オブジェクトの型を記述する [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) を返します。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 たとえば、 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md) オブジェクトが整数を指している場合、このメソッドによって返される [IDebugField](../../../extensibility/debugger/reference/idebugfield.md) 型によってその整数型が記述されます。  
  
## <a name="see-also"></a>参照  
 [IDebugPointerField](../../../extensibility/debugger/reference/idebugpointerfield.md)   
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
