---
title: BPERESI_FIELDS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- BPERESI_FIELDS
helpviewer_keywords:
- BPERESI_FIELDS enumeration
ms.assetid: dd7dd89c-1043-46a1-a929-099cc039c344
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: b1b5cba13e439c69b3502b00c6ae159b6af28178
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68153233"
---
# <a name="bperesi_fields"></a>BPERESI_FIELDS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

ブレークポイントの失敗した解決について取得する情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_BPERESI_FIELDS {   
   PERESI_BPRESLOCATION = 0x0001,  
   BPERESI_PROGRAM      = 0x0002,  
   BPERESI_THREAD       = 0x0004,  
   BPERESI_MESSAGE      = 0x0008,  
   BPERESI_TYPE         = 0x0010,  
   BPERESI_ALLFIELDS    = 0xffffffff  
};  
typedef DWORD BPERESI_FIELDS;  
```  
  
```csharp  
public enum enum_BPERESI_FIELDS {   
   PERESI_BPRESLOCATION = 0x0001,  
   BPERESI_PROGRAM      = 0x0002,  
   BPERESI_THREAD       = 0x0004,  
   BPERESI_MESSAGE      = 0x0008,  
   BPERESI_TYPE         = 0x0010,  
   BPERESI_ALLFIELDS    = 0xffffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 PERESI_BPRESLOCATION  
 `bpResLocation` [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体の (ブレークポイント解決の場所) フィールドを初期化または使用します。  
  
 BPERESI_PROGRAM  
 構造体のフィールドを初期化/使用し `pProgram` `BP_ERROR_RESOLUTION_INFO` ます。  
  
 BPERESI_THREAD  
 構造体のフィールドを初期化/使用し `pThread` `BP_ERROR_RESOLUTION_INFO` ます。  
  
 BPERESI_MESSAGE  
 構造体のフィールドを初期化/使用し `bstrMessage` `BP_ERROR_RESOLUTION_INFO` ます。  
  
 BPERESI_TYPE  
 `dwType`構造体の (ブレークポイントの種類) フィールドを初期化/使用し `BP_ERROR_RESOLUTION_INFO` ます。  
  
 BPERESI_ALLFIELDS  
 構造体のすべてのフィールドを初期化/使用し `BP_ERROR_RESOLUTION_INFO` ます。  
  
## <a name="remarks"></a>注釈  
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)構造体のどのフィールドを初期化するかを示すために、 [get解決情報](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)メソッドにパラメーターとして渡されます。  
  
 これらの値は、構造内のどのフィールドが使用され、 `BP_ERROR_RESOLUTION_INFO` その構造体が返されたときに有効であるかを示すためにも使用されます。  
  
 これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [BP_ERROR_RESOLUTION_INFO](../../../extensibility/debugger/reference/bp-error-resolution-info.md)   
 [GetResolutionInfo](../../../extensibility/debugger/reference/idebugerrorbreakpointresolution2-getresolutioninfo.md)
