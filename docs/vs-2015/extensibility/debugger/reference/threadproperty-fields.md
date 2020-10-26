---
title: THREADPROPERTY_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- THREADPROPERTY_FIELDS
helpviewer_keywords:
- THREADPROPERTY_FIELDS enumeration
ms.assetid: 5b88acb9-03ea-4c29-a788-f0087dccbe23
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: dc0e0f7cae4aed887809c22bda0cd6a9ed50307f
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68204801"
---
# <a name="threadproperty_fields"></a>THREADPROPERTY_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

スレッドに関する情報を取得するかどうかを指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
typedef DWORD THREADPROPERTY_FIELDS;  
```  
  
```csharp  
public enum enum_THREADPROPERTY_FIELDS {   
   TPF_ID           = 0x0001,  
   TPF_SUSPENDCOUNT = 0x0002,  
   TPF_STATE        = 0x0004,  
   TPF_PRIORITY     = 0x0008,  
   TPF_NAME         = 0x0010,  
   TPF_LOCATION     = 0x0020,  
   TPF_ALLFIELDS    = 0xffffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 TPF_ID  
 `dwThreadId` [Threadproperties](../../../extensibility/debugger/reference/threadproperties.md)構造体のフィールドを初期化/使用します。  
  
 TPF_SUSPENDCOUNT  
 `dwSuspendCount`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。  
  
 TPF_STATE  
 `dwThreadState`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。  
  
 TPF_PRIORITY  
 `bstrPriority`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。  
  
 TPF_NAME  
 `bstrName`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。  
  
 TPF_LOCATION  
 `bstrLocation`S 構造体のフィールドを初期化/使用し `THREADPROPERTIE` ます。  
  
 TPF_ALLFIELDS  
 すべてのフィールドを指定します。  
  
## <a name="remarks"></a>注釈  
 これらの値は、引数として [Getthreadproperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md) メソッドに渡さ [れ、どの](../../../extensibility/debugger/reference/threadproperties.md) フィールドを初期化するかを示します。  
  
 これらの値は `dwFields` 、使用される `THREADPROPERTIES` フィールドと有効なフィールドを示すために、構造体のメンバーでも使用されます。  
  
 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [THREADPROPERTIES](../../../extensibility/debugger/reference/threadproperties.md)   
 [GetThreadProperties](../../../extensibility/debugger/reference/idebugthread2-getthreadproperties.md)
