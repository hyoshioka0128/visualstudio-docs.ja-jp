---
title: 'IDebugPrimitiveTypeField:: GetPrimitiveType |Microsoft Docs'
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
helpviewer_keywords:
- GetPrimitiveType
- IDebugPrimitiveTypeField::GetPrimitiveType
ms.assetid: a186c922-bbfe-478c-a744-b21eb4672d8f
caps.latest.revision: 11
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 09be168816140781a87528f981d5d93460cec65f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68188123"
---
# <a name="idebugprimitivetypefieldgetprimitivetype"></a>IDebugPrimitiveTypeField::GetPrimitiveType
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このフィールドに関連付けられているプリミティブ型を取得します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
HRESULT GetPrimitiveType (  
   DWORD* pdwType  
);  
```  
  
```csharp  
int GetPrimitiveType (  
   out uint pdwType  
);  
```  
  
#### <a name="parameters"></a>パラメーター  
 `pdwType`  
 入出力プリミティブ型を表す [Corelementtype 列挙子](/dotnet/framework/unmanaged-api/metadata/corelementtype-enumeration) の値。  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返します `S_OK` 。それ以外の場合はを返し `S_FALSE` ます。  
  
## <a name="see-also"></a>参照  
 [IDebugPrimitiveTypeField](../../../extensibility/debugger/reference/idebugprimitivetypefield.md)
