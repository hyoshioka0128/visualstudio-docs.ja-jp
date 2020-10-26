---
title: IDebugProperty3::D estroyObjectID |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- IDebugProperty3::DestroyObjectID
helpviewer_keywords:
- IDebugProperty3::DestroyObjectID
ms.assetid: bd08f356-cc67-4717-98c9-c3d00cad2040
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 3a610cd5c947d77048e86b31c92298f6cc18607d
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68193424"
---
# <a name="idebugproperty3destroyobjectid"></a>IDebugProperty3::DestroyObjectID
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

このプロパティに関連付けられている一意の ID を破棄します。これは、呼び出し元が他のすべてのプロパティから一意にこのプロパティを識別しないことを示します。  
  
## <a name="syntax"></a>構文  
  
```cpp  
HRESULT DestroyObjectID(  
   void  
);  
```  
  
```csharp  
int DestroyObjectID();  
```  
  
## <a name="return-value"></a>戻り値  
 成功した場合はを返し `S_OK` ます。それ以外の場合はエラーコードを返します。  
  
## <a name="remarks"></a>注釈  
 デバッグエンジンがプロパティの一意の Id をサポートする必要がない場合 (既に内部的に一意に追跡しているため)、このメソッドに対して単にを返すことができ `E_NOTIMPL` ます。  
  
 呼び出し元が、このプロパティが他のすべてのプロパティで一意に識別されるようにする場合は、 [Createobjectid](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md) メソッドを呼び出すことで一意の id が作成されます。  
  
## <a name="see-also"></a>参照  
 [IDebugProperty3](../../../extensibility/debugger/reference/idebugproperty3.md)   
 [CreateObjectID](../../../extensibility/debugger/reference/idebugproperty3-createobjectid.md)
