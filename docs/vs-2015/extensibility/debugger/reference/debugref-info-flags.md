---
title: DEBUGREF_INFO_FLAGS |Microsoft Docs
ms.date: 11/15/2016
ms.prod: visual-studio-dev14
ms.technology: vs-ide-sdk
ms.topic: reference
f1_keywords:
- DEBUGREF_INFO_FLAGS
helpviewer_keywords:
- DEBUGREF_INFO_FLAGS enumeration
ms.assetid: 1b043327-302a-4f6d-b51d-f94f9d7c7f9d
caps.latest.revision: 12
ms.author: gregvanl
manager: jillfra
ms.openlocfilehash: 05a073b3663ff85fe3d68878999aaf1dfa9e0017
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "68198850"
---
# <a name="debugref_info_flags"></a>DEBUGREF_INFO_FLAGS
[!INCLUDE[vs2017banner](../../../includes/vs2017banner.md)]

デバッグ参照オブジェクトについて取得する情報を指定します。  
  
## <a name="syntax"></a>構文  
  
```cpp#  
enum enum_DEBUGREF_INFO_FLAGS {   
   DEBUGREF_INFO_NAME             = 0x00000001,  
   DEBUGREF_INFO_TYPE             = 0x00000002,  
   DEBUGREF_INFO_VALUE            = 0x00000004,  
   DEBUGREF_INFO_ATTRIB           = 0x00000008,  
   DEBUGREF_INFO_REFTYPE          = 0x00000010,  
   DEBUGREF_INFO_REF              = 0x00000020,  
   DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,  
   DEBUGREF_INFO_NONE             = 0x00000000,  
   DEBUGREF_INFO_ALL              = 0xffffffff  
};  
typedef DWORD DEBUGREF_INFO_FLAGS;  
```  
  
```csharp  
public enum enum_DEBUGREF_INFO_FLAGS {   
   DEBUGREF_INFO_NAME             = 0x00000001,  
   DEBUGREF_INFO_TYPE             = 0x00000002,  
   DEBUGREF_INFO_VALUE            = 0x00000004,  
   DEBUGREF_INFO_ATTRIB           = 0x00000008,  
   DEBUGREF_INFO_REFTYPE          = 0x00000010,  
   DEBUGREF_INFO_REF              = 0x00000020,  
   DEBUGREF_INFO_VALUE_AUTOEXPAND = 0x00010000,  
   DEBUGREF_INFO_NONE             = 0x00000000,  
   DEBUGREF_INFO_ALL              = 0xffffffff  
};  
```  
  
## <a name="members"></a>メンバー  
 DEBUGREF_INFO_NAME  
 構造体のフィールドを初期化/使用し `bstrName` ます。  
  
 DEBUGREF_INFO_TYPE  
 構造体のフィールドを初期化/使用し `bstrType` ます。  
  
 DEBUGREF_INFO_VALUE  
 構造体のフィールドを初期化/使用し `bstrValue` ます。  
  
 DEBUGREF_INFO_ATTRIB  
 構造体のフィールドを初期化/使用し `dwAttrib` ます。  
  
 DEBUGREF_INFO_REFTYPE  
 構造体のフィールドを初期化/使用し `dwRefType` ます。  
  
 DEBUGREF_INFO_REF  
 構造体のフィールドを初期化/使用し `pReference` ます。  
  
 DEBUGREF_INFO_VALUE_AUTOEXPAND  
 [値] フィールドには、この種類のオブジェクトの自動展開値 (使用可能な場合) が含まれている必要があります。  
  
 DEBUGREF_INFO_NONE  
 フラグが設定されていないことを示します。  
  
 DEBUGREF_INFO_ALL  
 フラグのマスクを示します。  
  
## <a name="remarks"></a>注釈  
 これらのフラグは、 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)構造体のどのフィールドを初期化するかを示すために、 [Enumchildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)メソッドと[getreferenceinfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)メソッドに渡されます。  
  
 構造体 `dwFields` のメンバーに、 `DEBUG_REFERENCE_INFO` 構造体が返されるときに使用されるフィールドと有効なフィールドを示すために使用されます。  
  
 これらの値は、ビットごとのを使用して組み合わせることができ `OR` ます。  
  
## <a name="requirements"></a>要件  
 ヘッダー: msdbg. h  
  
 名前空間: VisualStudio。  
  
 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll  
  
## <a name="see-also"></a>参照  
 [列挙](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)   
 [DEBUG_REFERENCE_INFO](../../../extensibility/debugger/reference/debug-reference-info.md)   
 [EnumChildren](../../../extensibility/debugger/reference/idebugreference2-enumchildren.md)   
 [GetReferenceInfo](../../../extensibility/debugger/reference/idebugreference2-getreferenceinfo.md)
