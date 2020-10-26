---
title: OBJECT_TYPE |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- OBJECT_TYPE
helpviewer_keywords:
- OBJECT_TYPE enumeration
ms.assetid: c4d246f9-8a98-44ec-b2bb-ff5c684f668e
caps.latest.revision: 10
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: fc23045fa70554133eba3a7f1326681bf31ea379
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68205141"
---
# <a name="object_type"></a>OBJECT_TYPE
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

式エバリュエーターからオブジェクトの型を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
typedef DWORD OBJECT_TYPE;  
```  
  
```csharp  
public enum enum_OBJECT_TYPE {   
   OBJECT_TYPE_BOOLEAN = 0x0,  
   OBJECT_TYPE_CHAR    = 0x1,  
   OBJECT_TYPE_I1      = 0x2,  
   OBJECT_TYPE_U1      = 0x3,  
   OBJECT_TYPE_I2      = 0x4,  
   OBJECT_TYPE_U2      = 0x5,  
   OBJECT_TYPE_I4      = 0x6,  
   OBJECT_TYPE_U4      = 0x7,  
   OBJECT_TYPE_I8      = 0x8,  
   OBJECT_TYPE_U8      = 0x9,  
   OBJECT_TYPE_R4      = 0xa,  
   OBJECT_TYPE_R8      = 0xb,  
   OBJECT_TYPE_OBJECT  = 0xc,  
   OBJECT_TYPE_NULL    = 0xd,  
   OBJECT_TYPE_CLASS   = 0xe  
};  
```  
  
## <a name="members"></a>メンバー  
 OBJECT_TYPE_BOOLEAN  
 オブジェクトがブール値であることを示します。  
  
 OBJECT_TYPE_CHAR  
 オブジェクトが文字であることを示します。  
  
 OBJECT_TYPE_I1  
 オブジェクトが1バイトの符号付き整数であることを示します。  
  
 OBJECT_TYPE_U1  
 オブジェクトが1バイトの符号なし整数であることを示します。  
  
 OBJECT_TYPE_I2  
 オブジェクトが2バイト符号付き整数であることを示します。  
  
 OBJECT_TYPE_U2  
 オブジェクトが2バイト符号なし整数であることを示します。  
  
 OBJECT_TYPE_I4  
 オブジェクトが4バイト符号付き整数であることを示します。  
  
 OBJECT_TYPE_U4  
 オブジェクトが4バイトの符号なし整数であることを示します。  
  
 OBJECT_TYPE_I8  
 オブジェクトが8バイト符号付き整数であることを示します。  
  
 OBJECT_TYPE_U8  
 オブジェクトが8バイト符号なし整数であることを示します。  
  
 OBJECT_TYPE_R4  
 オブジェクトが4バイトの浮動小数点数であることを示します。  
  
 OBJECT_TYPE_R8  
 オブジェクトが8バイトの浮動小数点数であることを示します。  
  
 OBJECT_TYPE_OBJECT  
 オブジェクトがオブジェクトであることを示します。  
  
 OBJECT_TYPE_NULL  
 オブジェクトが NULL であることを示します。  
  
 OBJECT_TYPE_CLASS  
 オブジェクトがクラスであることを示します。  
  
## <a name="remarks"></a>注釈  
 [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)メソッドおよび[createarrayobject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)メソッドに引数として渡されます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: ee  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [CreatePrimitiveObject](../../../extensibility/debugger/reference/idebugfunctionobject-createprimitiveobject.md)   
 [CreateArrayObject](../../../extensibility/debugger/reference/idebugfunctionobject-createarrayobject.md)
