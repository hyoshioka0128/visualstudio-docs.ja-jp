---
title: 'IDebugField:: Equal |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugField::Equal
helpviewer_keywords:
- IDebugField::Equal method
ms.assetid: 75369fe6-ddd3-497d-80d1-2488e6100e9f
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: aa630a6f2084f7ff79a9c89b685658cf694fcab9
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "62547313"
---
# <a name="idebugfieldequal"></a>IDebugField::Equal
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このメソッドは、このフィールドと指定したフィールドを比較し、等しいかどうかを比較します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT Equal(   
   IDebugField* pField  
);  
```  
  
```csharp  
int Equal(  
   IDebugField pField  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pField`  
 からこのと比較するフィールド。  
  
## <a name="return-value"></a>戻り値  
 フィールドが同じである場合、はを返し `S_OK` ます。 フィールドが異なる場合は、それ以外の場合は `S_FALSE.` エラーコードを返します。  
  
## <a name="see-also"></a>参照  
 [IDebugField](../../../extensibility/debugger/reference/idebugfield.md)
