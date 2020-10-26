---
title: MODULE_INFO_FIELDS |Microsoft Docs
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- MODULE_INFO_FIELDS
helpviewer_keywords:
- MODULE_INFO_FIELDS enumeration
ms.assetid: 8bed85f4-235f-4192-b58f-5fad7a4d7a78
author: acangialosi
ms.author: anthc
manager: jillfra
ms.workload:
- vssdk
dev_langs:
- CPP
- CSharp
ms.openlocfilehash: fa64147738a916d44b6924f193860f74bd10a855
ms.sourcegitcommit: 6cfffa72af599a9d667249caaaa411bb28ea69fd
ms.translationtype: MT
ms.contentlocale: ja-JP
ms.lasthandoff: 09/02/2020
ms.locfileid: "80714329"
---
# <a name="module_info_fields"></a>MODULE_INFO_FIELDS
デバッグモジュール情報のフラグを指定します。

## <a name="syntax"></a>構文

```cpp
enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
typedef DWORD MODULE_INFO_FIELDS;
```

```csharp
public enum enum_MODULE_INFO_FIELDS { 
   MIF_NONE              = 0x0000,
   MIF_NAME              = 0x0001,
   MIF_URL               = 0x0002,
   MIF_VERSION           = 0x0004,
   MIF_DEBUGMESSAGE      = 0x0008,
   MIF_LOADADDRESS       = 0x0010,
   MIF_PREFFEREDADDRESS  = 0x0020,
   MIF_SIZE              = 0x0040,
   MIF_LOADORDER         = 0x0080,
   MIF_TIMESTAMP         = 0x0100,
   MIF_URLSYMBOLLOCATION = 0x0200,
   MIF_FLAGS             = 0x0400,
   MIF_ALLFIELDS         = 0x07ff
};
```

## <a name="fields"></a>フィールド
 `MIF_NONE`\
 構造体のフィールドをすべて初期化/使用します。

 `MIF_NAME`\
 MODULE_INFO 構造体のフィールドを初期化/使用し `m_bstrName` ます。 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)

 `MIF_URL`\
 構造体のフィールドを初期化/使用し `m_bstrUrl` `MODULE_INFO` ます。

 `MIF_VERSION`\
 構造体のフィールドを初期化/使用し `m_bstrVersion` `MODULE_INFO` ます。

 `MIF_DEBUGMESSAGE`\
 構造体のフィールドを初期化/使用し `m_bstrDebugMessage` `MODULE_INFO` ます。

 `MIF_LOADADDRESS`\
 構造体のフィールドを初期化/使用し `m_addrLoadAddress` `MODULE_INFO` ます。

 `MIF_PREFFEREDADDRESS`\
 構造体のフィールドを初期化/使用し `m_addrPreferredLoadAddress` `MODULE_INFO` ます。

 `MIF_SIZE`\
 構造体のフィールドを初期化/使用し `m_dwSize` `MODULE_INFO` ます。

 `MIF_LOADORDER`\
 構造体のフィールドを初期化/使用し `m_dwLoadOrder` `MODULE_INFO` ます。

 `MIF_TIMESTAMP`\
 構造体のフィールドを初期化/使用し `m_TimeStamp` `MODULE_INFO` ます。

 `MIF_URLSYMBOLLOCATION`\
 構造体のフィールドを初期化/使用し `m_bstrUrlSymbolLocation` `MODULE_INFO` ます。

 `MIF_FLAGS`\
 構造体のフィールドを初期化/使用し `m_dwModuleFlags` `MODULE_INFO` ます。

 `MIF_ALLFIELDS`\
 構造体のすべてのフィールドを初期化/使用し `MODULE_INFO` ます。

## <a name="remarks"></a>解説
 これらの値は、 [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)構造体のどのフィールドを初期化するかを示すために、引数として[GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)メソッドに渡されます。

 これらの値は、使用される `MODULE_INFO` フィールドと有効なフィールドを示すために構造体でも使用されます。

 これらのフラグは、ビットごとのを使用して組み合わせることができ `OR` ます。

## <a name="requirements"></a>必要条件
 ヘッダー: msdbg. h

 名前空間: VisualStudio。

 アセンブリ: Microsoft.VisualStudio.Debugger.Interop.dll

## <a name="see-also"></a>関連項目
- [列挙型](../../../extensibility/debugger/reference/enumerations-visual-studio-debugging.md)
- [MODULE_INFO](../../../extensibility/debugger/reference/module-info.md)
- [GetInfo](../../../extensibility/debugger/reference/idebugmodule2-getinfo.md)
